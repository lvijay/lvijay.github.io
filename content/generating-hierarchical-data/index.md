---
title: "Generating hierarchical data"
description: "A method to generate self-documenting hierarchical data using Java 8 lambdas"
date: "2017-10-15T16:55:57.844Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/generating-hierarchical-data-f9510ce547d3
redirect_from:
  - /generating-hierarchical-data-f9510ce547d3
---

Edit on 2018–03–24: the number generating technique described in this article was first proposed by computer scientist Saul Gorn and it’s rightly named the [Gorn Address](https://en.wikipedia.org/wiki/Gorn_address) system.

Java 8’s lambdas make it easy to generate hierarchical data. Generating them in a self-documenting manner is easy too.

Given a hypothetical corporation with one CEO, ten VPs reporting to him/her, 4 senior managers reporting to each VP, 8 managers reporting to each senior manager, and finally, 9 plebs reporting to each manager. A simple way to generate employee IDs for these people is to assign the CEO employee id 1; assign each of the VPs ids 10, 11, …, 19; the senior managers under VP 12 could be assigned ids 120, 121, 122, and 123; and so on. Here’s where the self-documenting ids come in: given the id of a pleb as 14258 we know that this pleb is the 9th pleb reporting to manager with id 1425 whose the 6th report of senior manager 142 whose the 3rd report to VP 4, who, of course, reports to the sole CEO.

Here’s a straightforward way to do it

```
void generate(
        int ceoId,
        int nVPs,
        int nSrManagers,
        int nManagers,
        int nPlebs)
{
    long ceoid = 1;
    for (int ivp = 0; ivp < nVPs; ++ivp) {
        long vpid = ceoid * 10 + ivp;
        for (int ismgr = 0; ismgr < nSrManagers; ++ismgr) {
            long smgrid = vpid * 10 + ismgr;
            for (int imgr = 0; imgr < nVPs; ++imgr) {
                long mgrid = smgrid * 10 + imgr;
                for (int ipleb = 0; ipleb < nPlebs; ++ipleb) {
                    long plebid = mgrid * 10 + ipleb;

// do something with all these ids
                }
            }
        }
    }
}
```

This solution has several problems. It’s brittle: works only with a fixed hierarchy; it’s hard to understand—the id generation happens in multiple places; it’s sequential and hard to parallelize, and the business logic is tied with the generation.

#### Lambdas to the rescue

Given the same fixed hierarchy, here’s a simple way to solve this with lambdas.

```
void generate(
        int ceoId,
        int nVPs,
        int nSrManagers,
        int nManagers,
        int nPlebs)
{
    LongStream stream = LongStream.range(1, 1)
            .flatMap(ivp -> LongStream.range(ivp * 10, ivp * 10 + nVPs))
            .flatMap(ismgr -> LongStream.range(ismgr * 10, ismgr * 10 + nSrManagers))
            .flatMap(imgr -> LongStream.range(imgr * 10, imgr * 10 + nManagers))
            .flatMap(ipleb -> LongStream.range(ipleb * 10, ipleb * 10 + nPlebs));

    stream.forEach(plebid -> /* do stuff */);
}
```

This implementation gives us a stream which can be returned by the method and later used by any implementation that wishes to use the generated ids. Furthermore, adding a `.parallel()` will automatically parallelize the id generation.

#### Custom hierarchies

Of course, both solutions are brittle in that they solve fixed hierarchies. But, given the elegance of the lambda solution, to solve the custom hierarchy solution, I consider only lambdas.

The alert reader would have noted that both the above solutions have a fixed multiplicative factor of `10` but it will fail if the cardinality at any hierarchical level were above 10. Imagine, for instance, 3 hierarchical levels of 1 CEO, 2 VPs and 12 Senior Managers. The above implementations will generate VP ids as 10, 11. The Senior Managers of VP 10 will be 100, 101, …, **110, 111**; and the Senior Managers of VP 11 will be, **110, 111**, …. The ids collide. Thus the multiplicative factor of `10` cannot be hard-coded and must be a parameter of the generator function.

Our generator then has two input parameters: a list of cardinalities at each hierarchical level and multiplicative factors for these cardinalities.

```
void generate(int[] factors, int[] cardinalities) {
    LongStream generator = IntStream.range(0, factors.length)
            .boxed()
            .sequential()
            .reduce(LongStream.rangeClosed(1, 1),
                    (accumulator, idx) -> {
                        int i = idx.intValue();
                        int factor = factors[i];
                        int cardinality = cardinalities[i];

                        return accumulator.flatMap(v -> LongStream.range(v * factor, v * factor + cardinality));
                    },
                    (a, b) -> a);

    generator.forEach(/* do stuff */);
}
```

It’s assumed that the topmost hierarchical level has exactly one instance (this is the first argument to the reducer). Each intermediate level is then made by `flatMap`–ping over a generated LongStream. Note that the stream generator itself must be sequential though the final resulting stream may be run in parallel. Calling this function with invalid factors will return colliding values but now we have the invoker to blame for providing poor inputs. Poor inputs give poor results and the fault lies not in the method but in the caller.

#### Extracting higher level values

One thing the `for` loops had for them was that the implementation had access to each of the hierarchical levels at the same time. That’s not the case with the Stream solution, though. But we’ve gone this far so there’s no going back. So let’s write an extractor function that pulls out the hierarchical ids given a lower level id. We need the factors that were involved with the hierarchical generation.

```
LongFunction<long[]> extractor(int[] factors) {
    long[] divisiveFactors = new long[factors.length];
    divisiveFactors[factors.length - 1] = 1;
    for (int i = factors.length - 1; i > 0; --i) {
        divisiveFactors[i - 1] = divisiveFactors[i] * factors[i];
    }

    LongFunction<long[]> extractor = v -> {
        long[] hierarchicalIds = new long[factors.length + 1];

        for (int i = factors.length; i > 0; --i) {
            hierarchicalIds[i] = v / divisiveFactors[i - 1];
        }

        hierarchicalIds[0] = 1;

        return hierarchicalIds;
    };

    return extractor;
}
```

We continually divide each level by the product of factors before it. We precompute the factors by which we should divide each id to save runtime computational costs.

#### Sample Run

undefined

Here’s an example program that generates a hierarchical graph. The program generates a [graphviz](https://www2.graphviz.org/) file that generates the above image.

With above image as reference, if we have any node and its level, we can infer everything about it.

The next steps to this are generation of attributes at these hierarchical levels. To continue with our running example, suppose we want to generate a name for each level of the hierarchy.

But that’s for a future post.

P.S. if you have a more elegant method of extracting the ids, do share.
