# How to recreate the bug
This bug occurs on the Windows computer we're running the study on and my MacBook. So, you can probably test out some fixes on a MacBook and that will translate.
1. Open the project (this folder) in IntelliJ IDEA
2. Run the tests by hitting the play button in the upper right
3. 2 tests should have failed. The fix requires changing code in FastDateParser.java, so it would be best to navigate to that file to see how patches are making changes. To do this, use the search function by clicking the magnifying glass in the upper right, and typing in "FastDateParser.java".
4. There are two patches in the folder. The deceptiveAPR(2).patch will cause the bug we're interested in. To apply it, right click on the file in the project file tree on the left and click "Apply Patch". Click OK.
5. Run the tests again. 16 should fail. Uh oh!
6. Profit.

To undo a patch, you can click into the file that the patch was applied to and do a Ctrl/Command-Z. 

Applying the correctAPR.patch results in no failing tests, so at least there's that.

Speculation: the deceptive patch swaps out a guard call to Character.isHighSurrogate(c). I think that isHighSurrogate() may require some parsing behavior that is present in some IDE or JDK/Java default parsing settings. Additionally, changing the JDK to 8 causes other parse-related issues.
