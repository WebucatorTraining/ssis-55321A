# ssis-55321A

Used by Skillable to create lab instructions.

### Notes for Nat
These files were created using the markdown.py script in the courseware-sql repo.
This requires copying over all created markdown files and all images in the **Manual/Images** folder into the local **Images** folder.

After converting:
1. In **L03-control-flow-StepByStep.md**, tab in lines 107-116
2. In **L04-common-tasks-StepByStep.md**
   1. Move "If you are using a corporate email server, the To and From addresses should both be your email address." to line before an italicize.
   2. Unindent one level lines 182-187.
3. In **L06-transformations-StepByStep.md**, delete `\n` at line 155.
4. In **L07-making-packages-dynamic-StepByStep.md**, delete `\n` at lines 103 and 201 (with preceding 4 spaces).
5. **L08-containers-HighLevel.md** contained all the high-level and step-by-step instructions, and L08-containers-StepByStep.md contained none of it. Fix that.
6. In **L09-reliability-StepByStep.md**, delete lines 54 and 75, and tab in lines 64-66.
7. In **L10-deploying-StepByStep.md**, delete line 189.
8. Fix indenting in **L02-ssdt-HighLevel.md**, **L02-ssdt-StepByStep.md**, and **L10-deploying-StepByStep.md**. Search for content starting with “If you did not perform” and make sure that falls under the numbered item.
9. Search **\`([\w\s]+)\`** and replace with `<code class="nocopy">$1</code>` as per this note from David Behymer:
      ```
       our platform interprets backticks (`) as copyable text.  So, as things are now, you will see the copy icon next to all words that have the backticks.   Refer to the screenshot below for an example.   If you’re OK with that you can choose to leave it that way.  If not, you will need to replace the backticks with <code class="nocopy"> and </code>.  This will render the text highlighted in gray without the copy icon.
       ```
