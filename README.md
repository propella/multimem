multimem
========

Report Proportional set size (PSS) of a multi process program

Usage
-----

    multimem [pid]

Example

```
$ ./multimem $(pidof weston)
(PID) Name                                   SWAP      USS      PSS      RSS
----------------------------------------------------------------------------
(1000) weston                                   0    22504    36281    55708
  (1293) ssh-agent                              ?        ?        ?        ?
  (1462) weston-desktop-                        0     2188     3787     9832
    (2849) weston-terminal                      0     5312     7513    14924
      (2850) bash                               0     2108     2370     5864
        (22555) weston-smoke                    0     2416     3038     7384
        (22520) weston-simple-e                 0    14372    26144    41660
        (22507) weston-flower                   0     1524     2161     6524
  (1461) weston-keyboard                        0     2780     3884     9336
----------------------------------------------------------------------------
Total                                          ?0   ?53204   ?85178  ?151232
```

What is this?
-------------

I'm pretty sure there should be a similar tool to measure memory size (including PSS) used by a program with multi process. But I cannot find it. So I wrote this. Source code was derived from [smem](https://selenic.com/repo/smem).

If you specify pid, it shows the process tree and the memory usage for each. If you cannot access the memory map, the size is shown as "?".

Total size is shown on the bottom. But if you cannot access any child process, "?" is shown before the size because the total number is inaccurate.

References
----------

* ELC: How much memory are applications really using?: https://lwn.net/Articles/230975/
* smem: https://selenic.com/repo/smem
