# xtomato

Originally inspired from some very basic shellcode from
Thordur Bjornsson this time slicing of human time initiated
by computer application has grown a bit since it began.

The basic premise is

```
  (
    (
      work
      <short break>
    )
    repeat 4 times
    replace last <short break> with <long break>
  )
  repeat while working
```

...for optimal productivity.  For further details, see
http://en.wikipedia.org/wiki/Pomodoro_Technique .

One can create a $HOME/worklist file that helps
the computer prompt the human for what to work on.

It looks like this (indented for clarity here, the
'o project' must be left aligned and whitespace is
only supported as spaces at this time):

```
    o project weight=100
     o subproject1
      o details per subproject
        can even wrap around
     o subproject2
     o subproject3
    o project weight=200
```

And xtomato will automatically select the first project and the first
subproject for the first work task, presenting subsequent projects
and cycling through the subprojects of each project as applicable.

  "It takes the 'human time' out of deciding what to do next"

Note the only granularity is for project+subproject, anything under
subproject is included when displaying info about the task to work on.

If you have a desire to do:

```
   o client1
    o projects
     o subproject1
     o subproject2
     ...
    o maintenance
```

It will be necessary to rethink this as:

```
   o client1
    o projects-subproject1
    o projects-subproject2
     ...
    o maintenance
```

Also note, project and subprojects are currently only supported as a single
word.

This is an even-steven algorithm.

There is an in-progress weight system designed to work as the example
above indicates for specifying the weight of a given project.  This
will eventually be extended to subprojects.

The purpose of a 'weight' is to give a numeric value which, relative
to other numeric weights, determines how much time each project should
have given the typical hack time.  In the above example, if hack time
is typically 1000s then weight=100 will receive 660s and weight=200 will
receive 1320s.  Basically the formula goes like this:

```
	HACK * projectcount = totalhacktime

	projecthacktime = totalhacktime * ( weight / total_of_all_weights )
```

This is yet to be implemented but at least the program parses the weights.

Other use cases involve needing to get one 'round' of progress in given a
known hard stop scenario.

```
 xtomato -T $((60*30)) # 30min before hard stop
 xtomato -b            # berzerk mode (from doom) aka no breaks
```

Someday we can all say "pay me more to get more weight to a 'project'"
or even let others decide what weight the subprojects associated with
their desires get.

I personally feel much more productive while using this application now.

As always, if you feel the need to let me know what you think, especially
in the form of bugfixes, diffs, or pull requests, let me know at
todd@fries.net.

Thanks,
```
-- 
Todd Fries .. todd@fries.net .. twitter:@unix2mars .. github:toddfries

Label   | Data           | Notes
--------+----------------+------------------------------
Motto   | In support of  | free software solutions.
Phone   | 1.405.252.0702 | SMS/voice everywhere
Mobile  | 1.405.203.6124 | SMS/voice mobile only
Employer| self employed  | Free Daemon Consulting, LLC
Address | PO Box 16169   | Oklahoma City, OK 73113-2169
PGP     | 3F42004A       |
```
