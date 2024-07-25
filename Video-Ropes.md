### Beginning
Ropes are weird. Here is why - look at those three examples.
1. **In the first one:** the rope snaps.
2. **In the second one:** well, the rope snaps again.
3. **But in the third one:** the rope doesn't snap.

Why? Let me explain?
### Examples notion
1. **In the first example** the rope attaches to only one plank - thus it snaps.
2. **In the second example** I first build the rope and then an additional plank that attaches to the rope - but it snaps again.
3. **In the third example** I first build an additional plank and only then the rope. And here it doesn't snap!
### Explanation
I would like to call this **node reserve:**

1. **In the first example** the rope attaches to only one plank, so if the node fails - the rope snaps.
2. **In the second example** when placing the rope it didn't "knew" about an additional plank - it was introduced only after the rope placement. The rope "listens" to the amount planks when you place the rope. Here there was only one plank in the first place, so the outcome is the same as in the first example.
3. **In the third example** the rope has 2 duplicated nodes from each plank. So when one node fails - there is another one in **reserve**.

### With reactors
Here is the same thing but with reactors:
1. **With one plank** - you die.
2. **With the rope before an additional plank** - you die again.
3. **But with an additional plank before the rope** - it works like a charm!

### Conclusion
I hope this helped you to not kill your core in a violent **death.**
**Also** - this is a quite a nice base: new rush video incoming! Goodbye.