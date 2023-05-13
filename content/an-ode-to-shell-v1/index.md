---
title: "An Ode to Shell v1"
description: "The shell is the coolest thing out there. It is unmatched in terms of pedagogy — helping people learn concepts. And yet, people seem to…"
date: "2023-05-13T11:44:49.983Z"
categories: []
published: false
---

The shell is the coolest thing out there. It is unmatched in terms of pedagogy — helping people learn concepts. And yet, people seem to know very little of it. I figured, since I like complaining, I’d write this and complain that developers aren’t reading my post rather than complain about their ignorance (which is always unfair because ignorance isn’t a sin). This has the double benefit that I can now say, “I told you so,” and when people challenge me that I’m not doing anything about it, I can say, “go read my article”.

So, without much further ado, here we go. We’re going to cover the following “cool” industry topics:

-   MapReduce
-   Databases
-   Microservices
-   Benchmarking

(It’s possible some of these topics aren’t as cool as they once were but industry trends, like fashion trends, keep changing and I don’t pay much attention to them. After all, I’m someone who appreciates something as retro as the shell. And, if I’m able to do all right in this industry _despite_ eschewing trends — and thus avoiding the dreaded [FOMO](https://en.wikipedia.org/wiki/Fear_of_missing_out) — I argue it’s _because_ of the shell. The shell lets me understand the concepts behind whatever’s new and fashionable without getting bogged down by the details.)

### Preliminaries

Before we get into the details of the programs below, let’s go through a lightning tour of shell programs. The best way to understand the programs shown here is to run them. Run them, tweak them, run them again. In time you’ll be writing your own scripts and we can exchange notes.

**Quick note:** throughout this article, when I say shell, I mean the _bash_ shell. If you already know some other shell, great, skim through this section and see how the discussed concepts can be applied in your shell of choice.

Feel free to skip this section if you’re already familiar with basic shell primitives.

**Quick note 2:** for pedagogical reasons, I minimize the use of shell primitives. It’s a given that many of the scripts in this post can be done more concisely or differently than what’s shown. There are some things which are “wrong” in the technical sense but still justifiable in the same way that introductory mathematics courses teaching the numbers only discuss the Naturals (0,1,2,3…) without discussing the other infinite classes of numbers like Integers, Rationals, Reals, and Imaginary TK footnote.

Think of all shell programs as being functions which accept arguments and return some output. All their arguments are strings and all their return types are strings. All shell scripts, then, are of the form program arg1 arg2 arg3… argN. The args are interpreted based on what program is.

#### Some basic programs

`cat` — prints each given input file   
`man` — the reference manual for most shell programs  
`echo` — outputs its arguments, separated by spaces, terminated with a newline  
`rev` — reverses a line characterwise  
`sort` — sorts, merges, or compares all the lines from the given files

There are others but we’ll look into them as we go.

#### Some shell primitives

`>` redirect — writes its input to a file  
`|` pipe — passes the output of another program to the next one  
`'` quote — quotes its arguments, preventing their evaluation  
`#` comment — the shell ignores everything that follows until the end of the line

There are others but we won’t use them. Once you’ve played with these examples, explore them on your own.

#### Using the above shell examples

For all our examples, we’ll need some files to act on. Let’s create them using the shell.

For our first file, we’ll create a file, named `digits`, containing the digits 0–9 on one line like so:  
`$ echo 0 1 2 3 4 5 6 7 8 9 > digits`

`echo` repeats its arguments  
`>` writes its input to the file `digits`. In this case, it so happens that the input to `>` is the output of echo.

You can print the file using `cat`

```
$ cat digits
0 1 2 3 4 5 6 7 8 9
```

If you want to repeat the contents of `digits`, just pass it twice to `cat`.

```
$ cat digits digits
0 1 2 3 4 5 6 7 8 9
0 1 2 3 4 5 6 7 8 9
```

Using just the digits 0–9 isn’t sufficient. Let’s change things a little. Let’s also save the digits in reversed order. We _could_ just type it out in reverse, but why type when the shell can do it for you? We’ll instead use the `rev` program to do our work. (Programming principle: DRY — don’t repeat yourself.)

```
$ rev digits
9 8 7 6 5 4 3 2 1 0
```

Let’s save the output of the above program to a file named `stigid`, which is “digits” reversed. (Shell programs are full of inside jokes like this. See, for instance the program, `[tac](https://www.gnu.org/software/coreutils/manual/coreutils.html#tac-invocation)`. It’s the same as `cat` but prints the output in order of reversed lines.)  
`$ rev digits > stigid`

Now, we can `cat` both these files

```
$ cat stigid digits
9 8 7 6 5 4 3 2 1 0
0 1 2 3 4 5 6 7 8 9
```

If you’ve followed until now, you’re ready for the second shell primitive, the `|` (read as “pipe”). The pipe operator is a way for one program to communicate with the next. (Get it? It acts as a _pipe_.)

Once we’ve `cat`’d the above two files, we can send it to `sort` which will sort the lines. Like so:

```
$ cat stigid digits | sort
0 1 2 3 4 5 6 7 8 9
9 8 7 6 5 4 3 2 1 0
```

Even if you `cat` several outputs, sort will sort the lines as you expect.

```
$ cat stigid digits stigid digits stigid | sort
0 1 2 3 4 5 6 7 8 9
0 1 2 3 4 5 6 7 8 9
9 8 7 6 5 4 3 2 1 0
9 8 7 6 5 4 3 2 1 0
9 8 7 6 5 4 3 2 1 0
```

Note that sort sorts on the basis of the _first column_ of each line, so in the above, all the lines were sorted by comparing `0`’s and `9`’s.

We’ll consider more complex examples and the other primitives, `#` and `'`, as we get into the actual concepts.

### How to read this post

> “The only way to learn a new programming language is by writing programs in it.” — Brian Kernighan and Dennis Ritchie, _The C Programming Language_

Open up a bash shell terminal, copy-paste the samples into your terminal; then explore, experiment, discover.

### MapReduce

Let’s quickly recap what MapReduce does before we look at replicating it on the shell. I will also add that practically every shell program is an implementation of the MapReduce paradigm.

In MapReduce, you have an input which you convert (or transform or, you know, _map_) into another form, doing this as many times as you feel necessary, before finally aggregating the results. This aggregation is called, you’ve guessed it, _reduction_.

The classic, “_Hello, World!_” example of a MapReduce program is a word counter. Given a large corpus of words, you write a MapReduce program whose task it is to count the frequency of occurrence of each word. As a negative example, i.e. how _not_ to go about learning MapReduce, I refer you to the Apache MapReduce Tutorial page: [https://hadoop.apache.org/docs/current/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html](https://hadoop.apache.org/docs/current/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html).

Let’s now do word count using the lowly shell.

First, we’ll create our sample input and, in the process, meet our third shell primitive, `'`, the single quote.

```
$ echo 'hello
world
hello
goodbye
cruel
WORLD' > input.txt
```

The `'` lets us generate a string that spans multiple lines. We `echo` this into a file named `input.txt`.

Here’s how to do a word count on this input:

```
$ cat input.txt | sort | uniq -c
   1 WORLD
   1 cruel
   1 goodbye
   2 hello
   1 world
```

Let’s break it down. The first part, `cat input.txt`, should be obvious so I won’t belabor it. What do we get when passing it to `sort`?

```
$ cat input.txt | sort
WORLD
cruel
goodbye
hello
hello
world
```

As one might expect, the output of `sort` is sorted. And, as readers familiar with ASCII are no doubt aware, the uppercase characters are sorted before the lowercase ones.

Next, we have the program `uniq` TK to “report or omit repeated lines”. However, when invoked with the argument `-c`, uniq (TK monospace) _counts_ how many times it’s seen every occurrence in its input.

And with just three programs — `cat`, `sort`, and `uniq` — we have a simple word counter in shell.

Now, suppose you want the same word counter but you want to count words in a case-insensitive manner? Right now, we print `WORLD 1` and `world 1` which, you feel, isn’t ideal. In MapReduce terms, you need to introduce a new mapper. In shell terms, you need to introduce one program in the middle. We’ll get into the details after we see the solution:

```
$ cat input.txt | tr '[:upper:]' '[:lower:]' | sort | uniq -c
   1 cruel
   1 goodbye
   2 hello
   2 world
```

This introduces the program `tr`. It’s short for _tr_anslate and does just that. In the above, program, it converts all uppercase characters to lowercase characters. Below I print the output of `tr` alone.

```
$ cat input.txt  | tr '[:upper:]' '[:lower:]'
hello
world
hello
goodbye
cruel
world
```

Of course, this is the simplest sample. You can do this and much more.

### Databases

The shell allows you to explore databases without concerning yourself with SQL or setting up a database. Many a time, I’ve actually used the shell to extract answers from log files which would have otherwise taken too long just to setup.

We’ll be looking at the following aspects of databases:  
⒈ Projection (select only some columns from the table)  
⒉ Filtering (removing unwanted rows, selecting only some rows)  
⒊ Joins, including  
⒊⒈ INNER JOIN  
⒊⒈⒈ Query Planning  
⒊⒉ LEFT OUTER JOIN  
⒊⒊ RIGHT OUTER JOIN  
⒊⒋ FULL OUTER JOIN

As with all database tutorials, let’s first setup our data. In true shell-ian fashion, our tables will be files, they’ll have a schema but we’ll have to keep it all in our heads. We’ll use the reference dataset from MySQL. For more details about the dataset, see [https://dev.mysql.com/doc/employee/en/employees-introduction.html](https://dev.mysql.com/doc/employee/en/employees-introduction.html). (It’s licensed at [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/), the same as this post.)

We’ll look at the tables and their schemata as we go on.

#### Projection

Of course, we’ve already seen the simplest SQL projection possible. The equivalent of `SELECT *` from a table is just `cat`. What we’re really interested in is selecting only _particular_ columns from the table. It’s time to look at our first table. The `employees` table gives us this. Below is a sample of our table.

```
$ head load_employees.data 
10001 1953-09-02 Georgi Facello M 1986-06-26 
10002 1964-06-02 Bezalel Simmel F 1985-11-21 
10003 1959-12-03 Parto Bamford M 1986-08-28 
10004 1954-05-01 Chirstian Koblick M 1986-12-01 
10005 1955-01-21 Kyoichi Maliniak M 1989-09-12 
10006 1953-04-20 Anneke Preusig F 1989-06-02 
10007 1957-05-23 Tzvetan Zielinski F 1989-02-10 
10008 1958-02-19 Saniya Kalloufi M 1994-09-15 
10009 1952-04-19 Sumant Peac F 1985-02-18 
10010 1963-06-01 Duangkaew Piveteau F 1989-08-24
```

The table’s schema is `employee_id`, `birth_date`, `first_name`, `last_name`, `gender`, `hire_date`. As is typical in the shell, the columns are space-separated. This is also the time to introduce the `head` program to “output the first part of files”. TK By default, `head` prints the first ten lines of each of its given files and that’s what we see.

The entire table has a little over three hundred thousand lines (300,024 to be exact) so we will use `head` most of the time. The full file is available for you to download at TK. It’s the same file as MySQL’s [load\_employees.dump](https://github.com/datacharmer/test_db/blob/master/load_employees.dump) with the SQL bits removed. The data along with the script that removed the SQL is also available in my repository named TK.

Let’s execute the equivalent of `SELECT employee_id, first_name, gender`:

```
$ cat load_employees.data | head | cut -d' ' -f1,3,5
10001 Georgi M
10002 Bezalel F
10003 Parto M
10004 Chirstian M
10005 Kyoichi M
10006 Anneke F
10007 Tzvetan F
10008 Saniya M
10009 Sumant F
10010 Duangkaew F
```

`cut`’s documentation says it can “remove sections from each line of files” and that’s exactly what we’ve done. As before, we only read the first ten lines of the file. `cut` take any character as its delimiter, this is specified above with the argument `-d' '` which tells `cut` to use the space character as its delimiter; the argument `-f` specifies which fields cut must retain in every line, in this case, we retain the columns 1, 3, and 5.

#### Filtering

Most of the time when we query a database (or any data source) we are interested in extracting only _some_ portions of it. Portions that match some criteria we’re interested in. Given what we know about the employee table’s schema, let’s invent some queries and then go ahead and execute them.

The queries will be:  
⒈ Find all male employees and  
⒉ Find the employee\_ids and last names of all female employees employed after the year 2000

Interested readers should try to solve it by themselves before looking at the answers below. Typically your approach will differ from mine and it’s always fun to exchange notes.

**⒈ Find all male employees**

```
$ cat load_employees.data | grep ' M [12]' | head
10001 1953-09-02 Georgi Facello M 1986-06-26 
10003 1959-12-03 Parto Bamford M 1986-08-28 
10004 1954-05-01 Chirstian Koblick M 1986-12-01 
10005 1955-01-21 Kyoichi Maliniak M 1989-09-12 
10008 1958-02-19 Saniya Kalloufi M 1994-09-15 
10012 1960-10-04 Patricio Bridgland M 1992-12-18 
10013 1963-06-07 Eberhardt Terkki M 1985-10-20 
10014 1956-02-12 Berni Genin M 1987-03-11 
10015 1959-08-19 Guoxiang Nooteboom M 1987-07-02 
10016 1961-05-02 Kazuhito Cappelletti M 1995-01-27
```

Say hello to `grep`. Probably the shell command I most use. According to its documentation, `grep` “print lines that match patterns”. TK Its manual spans 592 lines. (At 30 lines a page, that’s 19 pages.) `grep` takes a pattern as its first argument and (in this case) considers its input the data coming through the pipe. For simplicity, we only print the first ten lines.

Let’s take a look at our `grep` pattern in more detail. The fun thing about the shell is you typically come up with inventive (and non-intuitive) ways to get your answers. In this case, rather than finding a way to say the equivalent of `WHERE gender='M'` we’ve done something a bit different. Let’s take a look at our data. All our data is space separated and none of the names have numbers in them. What we’ve done is tell `grep` to pick out all lines which have the character ‘M’ surrounded by spaces on either side followed by `[12]`. `grep` interprets the brackets (`[` and `]`) as defining a _character class._ In this case,`[12]` matches _either_ `1` _or_ `2` and nothing else. As it so happens, `hire_date` succeeds `gender`, and since all dates either start with 1 or 2 (twentieth or twenty-first century), the `grep` pattern matches only the `gender` rows.

**⒉ Find the employee\_ids and last names of all female employees employed after the year 2000**

```
$ cat load_employees.data | grep ' F 2' | cut -d' ' -f1,4
60134 Rathonyi
72329 Luit
205048 Alblas
222965 Perko
226633 Benzmuller
422990 Verspoor
499553 Delgrande
```

This solution should be self-explanatory because it introduces nothing new. I’ll leave understanding it as an exercise.

#### JOINS

Databases would be almost useless if not for joins. For our exploration of joins, we’ll be using the shell program named, funnily enough, `join`. The man page says it can “join lines of two files on a common field” TK ([https://www.gnu.org/software/coreutils/join](https://www.gnu.org/software/coreutils/join)) which is exactly what a database join does. We’ll look at each JOIN variant below.

It’s time to introduce two more tables: `departments` and `department_employees`.

`departments` is a small table with only two columns: `department_id` and `department_name`. The second table, `department_employees`, is the mapping table with the following columns: `employee_id`, `department_id`, `from_date`, `to_date`.

Here’s what both look like. The `departments` table is small. It only has 9 rows which we’ve shown in full.

```
$ cat load_departments.data
d001 Marketing 
d002 Finance 
d003 Human_Resources 
d004 Production 
d005 Development 
d006 Quality_Management 
d007 Sales 
d008 Research 
d009 Customer_Service
```

`department_employees` contains at least as many rows as there are employees (employees who have worked in multiple departments will be listed multiple times). As it happens, the table has 331,603 rows which is 31,579 more than the number of employees. Here’s a sample of the table:

```
$ tail load_dept_emp.data 
499991 d009 1997-02-11 9999-01-01 
499992 d001 1995-05-31 9999-01-01 
499992 d003 1987-05-10 1995-05-31 
499993 d004 1997-04-07 9999-01-01 
499994 d004 1993-02-22 1993-10-27 
499995 d004 1997-06-02 9999-01-01 
499996 d004 1996-05-13 9999-01-01 
499997 d005 1987-08-30 9999-01-01 
499998 d002 1993-12-27 9999-01-01 
499999 d004 1997-11-30 9999-01-01
```

The last column indicates the date on which the employee left the department. If the employee is still in that department, the year is set to `9999–01–01`. Notice that `employee_id` `499992` (Siamak Salverda) repeats twice. She was originally in department `d003` (Human Resources) until May 1995 when she shifted to department `d001` (Finance). It’s also a good time to meet `tail`, a program to “output the last part of files” (https://www.gnu.org/software/coreutils/tail) TK. Like `head`, `tail` prints the last ten lines of its input by default.

**_MapReduce exercise_**_:_ list all employee(s) who have changed departments.

**INNER JOIN  
**An inner join combines two tables on the basis of what both of them have in common. This is exactly what `join` does.

`join` requires that its data be sorted on the join field (the column in common between the tables). This is reasonable when you think about it. I hope you do because I’m leaving the answer as an exercise. (Hint: how would _you_ write `join`? Is it easier when the data is sorted?) `join` expects its files to be sorted lexicographically (alphabetically) as opposed to numerically. To satisfy this we’ll first sort our three tables on their join fields.

**Query**: find the names and birthdays of all employees still working in Marketing.

Let’s start simple. First we’ll find the Marketing department’s `department_id`. We get that as below:

```
$ cat load_departments.data | grep Marketing
d001 Marketing
```

Next, we’ll use this information to join the `employees` and `department_employees`but first we’ll sort them lexicographically on their join field.

```
$ cat load_dept_emp.data | sort > load_dept_emp.data.sorted
$ cat load_employees.data | sort > load_employees.data.sorted
```

Below is the result. The full result set has 14,842 rows of which we only see the last ten.

```
$ cat load_dept_emp.data.sorted | grep d001 | grep 9999-01-01 | join - load_employees.data.sorted | cut -d' ' -f6-8 | tail
1964-05-15 Gully Hebert
1964-08-21 Arunas Tokunaga
1960-08-10 Yishai Cesareni
1960-11-02 Zengping Rindone
1962-08-06 Ranga DuCasse
1956-06-25 Spyrose Waymire
1960-10-13 Jaewon Paludetto
1962-01-06 Along Schaap
1960-01-12 Amalendu Apsitis
1952-06-18 Matt Motley
```

But that’s cheating, I hear you say. In a real database, the three tables would be INNER JOIN’d in one SQL statement. While true, remember, we’re only trying to achieve understanding, not replicate the database. That said, we’ll do a three table join in one statement after we’ve analyzed the above shell script.

The first part, `cat load_dept_emp.data.sorted | grep d001 | grep 9999-01-01` brings in the data we want, namely, all employees in Marketing (`d001`) who’re still in the department (date: `9999-01-01`). It looks like below:

```
$ cat load_dept_emp.data.sorted | grep d001 | grep 9999-01-01 | tail
99751 d001 1989-08-02 9999-01-01 
99765 d001 1989-11-03 9999-01-01 
99784 d001 1994-08-19 9999-01-01 
99869 d001 1991-09-21 9999-01-01 
99884 d001 1986-04-14 9999-01-01 
99933 d001 1985-03-06 9999-01-01 
99936 d001 1995-04-11 9999-01-01 
99950 d001 2002-07-13 9999-01-01 
99965 d001 1990-04-10 9999-01-01 
99988 d001 1999-04-21 9999-01-01
```

The second part, `join - load_employees.data.sorted`, is the more interesting part. `join` as we’ve discussed, takes two arguments, both files to join. In this case, the second file is `load_employees.data.sorted` which contains all the employee data. The first file, listed as `-` is not a file in the sense of being saved as a named file on disk, rather, it tells `join` to treat the input received from the pipe as a file. The output of the first two parts is shown below:

```
$ cat load_dept_emp.data.sorted | grep d001 | grep 9999-01-01 | join - load_employees.data.sorted | tail
99751 d001 1989-08-02 9999-01-01  1964-05-15 Gully Hebert F 1989-08-02 
99765 d001 1989-11-03 9999-01-01  1964-08-21 Arunas Tokunaga M 1989-04-21 
99784 d001 1994-08-19 9999-01-01  1960-08-10 Yishai Cesareni F 1992-12-27 
99869 d001 1991-09-21 9999-01-01  1960-11-02 Zengping Rindone F 1991-09-21 
99884 d001 1986-04-14 9999-01-01  1962-08-06 Ranga DuCasse M 1986-04-14 
99933 d001 1985-03-06 9999-01-01  1956-06-25 Spyrose Waymire F 1985-03-06 
99936 d001 1995-04-11 9999-01-01  1960-10-13 Jaewon Paludetto M 1994-07-02 
99950 d001 2002-07-13 9999-01-01  1962-01-06 Along Schaap M 1990-03-04 
99965 d001 1990-04-10 9999-01-01  1960-01-12 Amalendu Apsitis M 1990-04-10 
99988 d001 1999-04-21 9999-01-01  1952-06-18 Matt Motley M 1994-06-14
```

The lines overflow so you’ll need to squint a bit. Or, you might find the below image more convenient. It also highlights in red the data `grep` has matched.

The output of \`cat load\_dept\_emp.data.sorted | grep d001 | grep 9999–01–01 | join — load\_employees.data.sorted | tail\`

As you can see the output of `join`is the _join field_, `employee_id` in this case, followed by the columns of the first table (filtered rows from `load_dept_emp.data)` followed by all columns of the second table (`load_employees.data`) excluding the join field.

Now let’s join the three tables in one command. Recall that `join` requires sorted inputs and note that that means we cannot join `load_departments.data` with `load_dept_emp.data` because they are sorted on different keys. Thus, before we join with a single line, we’ll sort `load_dept_emp.data` on `department_id` pipe it forward, join it, then sort it again. (This is very inefficient but we’ll ignore inefficiencies for now. A better way would be to sort the file and save it in a temporary file and use that. See also the following section §Query Planning TK.)

```
$ cat load_dept_emp.data | sort -k2 | join -22 load_departments.data - | grep Marketing | sort -k3 | join -13 - load_employees.data.sorted | grep 9999-01-01 | cut -d' ' -f7-9 | tail
1964-05-15 Gully Hebert
1964-08-21 Arunas Tokunaga
1960-08-10 Yishai Cesareni
1960-11-02 Zengping Rindone
1962-08-06 Ranga DuCasse
1956-06-25 Spyrose Waymire
1960-10-13 Jaewon Paludetto
1962-01-06 Along Schaap
1960-01-12 Amalendu Apsitis
1952-06-18 Matt Motley
```

Take a second to verify that both times we’ve received the same output.

We see a new variant of `sort` above. Everything else should be familiar. We pass it the argument `-k2`. This tells `sort` to sort its data on its _second_ column.

#### Query Planning

In our final script of the last section, we had a few choices. Inner joins are commutative, meaning the order in which you join them doesn’t matter. So if you can join tables A and B, joining them as A⋈B will yield the same results as B⋈A where ⋈ is the mathematical symbol for an INNER JOIN. While we actually did the joins in the order `load_dept_emp.data ⋈ load_departments.data ⋈ load_employees.data`, filtering before every join, we could’ve done the joins in another order and still received the same result. Consider below, for example:

```
$ join load_dept_emp.data.sorted load_employees.data.sorted | sort -k2 | join -12 - load_departments.data | grep Marketing | grep 9999-01-01 | sort -k2 | cut -d' ' -f5-7 | tail
1964-05-15 Gully Hebert
1964-08-21 Arunas Tokunaga
1960-08-10 Yishai Cesareni
1960-11-02 Zengping Rindone
1962-08-06 Ranga DuCasse
1956-06-25 Spyrose Waymire
1960-10-13 Jaewon Paludetto
1962-01-06 Along Schaap
1960-01-12 Amalendu Apsitis
1952-06-18 Matt Motley
```

Once again, take a second to assert that the outputs are the same.

Suppose we label the three tables as follows:

A ← load\_departments.data  
B ← load\_dept\_emp.data  
C ← load\_employees.data

A and C cannot be joined with each other. All other combinations are possible.

For our first join, we did A ⋈ B ⋈ C. and we did B ⋈ C ⋈ A for the second. (Joins associate left, so read “A ⋈ B ⋈ C” as first joining A with B, getting a result, and then joining that with C. In precedence order, it’s: (A ⋈ B) ⋈ C.)

The second thing to observe is that filtering reduces the size of the tables.

⒝ is easier to answer so we’ll first address it. We’ve seen two scripts which give the same results, if they have different execution times, then ⒝ is answered affirmatively. (Interestingly, we can conclude nothing if both give the same execution time. Why not? Left as exercise.)

On my computer, I get the following execution times for both scripts:

```
## The shell ignores everything from a # until end-of-line
 
# join = A ⋈ B ⋈ C
$ time join -22 load_departments.data load_dept_emp.data.sorted-f2 | sort -k3 | join -13 - load_employees.data.sorted | grep 9999-01-01 | grep Marketing | cut -d' ' -f7-9 | tail -1
1952-06-18 Matt Motley

real    0m1.138s
user    0m1.595s
sys     0m0.127s

# join = B ⋈ C ⋈ A
$ time join load_dept_emp.data.sorted load_employees.data.sorted | sort -k2 | join -12 - load_departments.data | grep Marketing | grep 9999-01-01 | sort -k2 | cut -d' ' -f5-7 | tail -1
1952-06-18 Matt Motley

real    0m1.143s
user    0m1.356s
sys     0m0.151s
```

`time` is a program which gives you the time a program took to execute. (It doesn’t tell you the time, `date` does that.) It prints three categories of time: real, user, and sys. real gives the amount of time the program took from start to finish. We won’t go into user and sys here. Between the two joins there’s only a 4% difference in time which, for all intents, is probably insignificant.
