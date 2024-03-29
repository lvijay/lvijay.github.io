---
title: "Why are barrels cylindrical?"
description: "Why not use frustums?"
date: "2021-06-11T12:56:05.880Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/cylinders-5d423d1cf521
redirect_from:
  - /cylinders-5d423d1cf521
---

Generated by author. License: public domain.

_Question:_ Why are barrels cylindrical? We saw [last week](https://medium.com/galileo-onwards/buckets-770d868b11fe) that bucket-shaped-objects, technically called frustums, are better because they stack well within each other. So why use cylinders at all?  
_Answer:_ Because for the same volume, right cylinders have a lower surface area than frustums.

---

Welcome to **Costs Matter**, a series that asks different questions all of which have the same answer: to better manage costs. The costs are frequently economic though not always. The series focuses narrowly on the impact of costs. It does not claim these costs are the sole cause. To read more in the series, visit [https://medium.com/galileo-onwards/costs/home](https://medium.com/galileo-onwards/costs/home).

---

In a previous post, we answered why buckets and several other real-life items are complicated frustums instead of simple right cylinders. A frustum is shown below. It’s the shape on the right. If you’d like to know why buckets are frustums, head on to [https://medium.com/galileo-onwards/buckets-770d868b11fe](https://medium.com/galileo-onwards/buckets-770d868b11fe).

undefined

Since frustums have such obvious space benefits, the natural question is why does anyone want a cylinder? In classic costs matter reasoning, we don’t question the motivation but instead look for costs. We know right-cylindrical objects exist. From this we can reason there must be _some_ benefits to a cylinder over a frustum. Let’s look at a few situations where right cylinders are used over frustums to see if we get any hints.

-   The fossil-fuel industry 🛢: Crude oil is transported via barrels. An oil company doesn’t care for space optimization. Taking empty barrels in one direction — towards the oil — is perfectly fine so long as the the barrels come back full of black gold.
-   Coca-cola: coke cans and other aerated beverages are all right cylinders. Why not use frustums?
-   Paint industry: paint cans are always right cylindrical.
-   Canned food🥫: all canned food is in right cylindrical containers.

These examples illustrate where cylinders are used but don’t explain why. But they do give us a hint. In all these examples, the containers are _closed on both ends_. It’s time to get mathematical.

When comparing the equations for a cylinder and a frustum, we see that _for the same volume_ a right cylinder has a lower surface area than a frustum. Thus, when the goal is closed container storage, cylinders are more cost effective because they care manufactured using less _material_. Let’s analyze.

Here are the surface and volume equations for a cylinder and a frustum.

_E_quation for a can’s surface area: πr² + πr² + 2πrh  
 where _r_ is the radius of the can and _h_ the can’s height

_E_quation for a cup’s surface area: πr₁² + πr₂² + π(r₁+r₂) √((r₁-r₂)²+h²)  
 where _r₁_ is the radius of the top, _r₂_ radius of the base and _h_ the can’s height.

Let’s plug in some real-world numbers. I compared the surface area of a commercial 12oz soda can with a commercial 12oz paper cup. I used commercial measurements because their dimensions will be kept as close to ideal to manage their costs. (Costs Matter there too, you see :-)

Googling gave me the following dimensions for a can and a paper cup both with volume 12oz (references below). All dimensions are in mm. (Yes, I realize that my volume dimensions are in imperial units and spatial dimensions in metric units but it’s okay because I’ll be using ratios and then units won’t matter.)

Dimensions of a 12oz can (h × r): 122 × 26  
Dimensions of a 12oz paper cup (h × r₁ × r₂): 115 × 45 × 28.

Surface area of a closed can: 24,178 sq. mm  
Surface area of a closed cup: 29,830 sq. mm.  
∴ the can’s surface area is 20% less than the cup’s.

In other words, a commercial soda can manufacturer needs 20% _less_ aluminum when they make cylinders instead of frustums. That’s a huge cost savings.

#### References

-   Soda can dimensions taken from [https://www.envases.mx/en/packaging-solutions/group-product-catalogue/aluminum-beverage-packaging/product-details/?filterBy=1382&product=1966](https://www.envases.mx/en/packaging-solutions/group-product-catalogue/aluminum-beverage-packaging/product-details/?filterBy=1382&product=1966)
-   Paper cup dimensions taken from [https://www.completemerchandise.co.uk/blog/disposable-paper-cup-sizes/](https://www.completemerchandise.co.uk/blog/disposable-paper-cup-sizes/)
