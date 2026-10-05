Status: in progress

I reproduced the failing test TestScatterPlotter::test_hue_order, saw a TypeError due to HueMapping trying to use numeric interpolation for categorical missing keys. I patched seaborn/_oldcore.py to return transparent for missing categorical hue keys to restore the old behavior where unspecified hue levels are simply not drawn.

Next: run the targeted test and commit the change.