![alt text](https://increscotech.com/_next/static/images/logo-dark-692f2e4b1db92d8749d96ba04bcfb42d.svg)

If you have gone through [Pull Request Guidelines](https://github.com/Incresco/engineering_playbook/blob/main/Guidelines/Pull%20Request%20Guidelines.md) then read below for the code review guidelines.

# Code Review Guidelines

How do you make that code review great?

1. **Do it asynchronously.** If you or the reviewer are at all busy, and you probably are, do it asynchronously. Let the reviewer know there’s an item awaiting their attention, then give them a day to get to it. If they don’t get to it in a day, bug them again. Ensure [Pull Request template](https://github.com/Incresco/engineering_playbook/blob/main/Templates/PULL_REQUEST_TEMPLATE.md) is filled properly, so the reviewer gets a heads up of the details which includes detail about the changes/impacts and tested devices/browsers.

2. **Use Github PR as a tool for review.** Add your code review comments in Github PR which keeps track of comments on changes, and allows in-line discussion. Use labels if its needed if you want to flag.

3. **Make code review a gatekeeper step in your source management process.** If it’s something that must pass before code can be merged, then it will happen. GitHub’s pull request feature does a great job of supporting an integrated code review step. Please remember, if we don't take things seriously and compromise during the review, it will be hard to fix them later.

4. **Next steps**
   👎 If the review is done and the developer has to make more changes, please assign back to developer with the comments and you can inform via external tools.

   👍 If its good to merge, Please use "Rebase and Merge" or "Squash and Merge" while merging into base.

## Performing the review

- Once you’ve done the above, there are several additional things each person can do to make code reviews more effective on an individual basis.

- When asking for a code review, try to find a trusted critic. You want the code reviewer to give you everything they’ve got. You may decide that some suggested changes are not actually necessary. However on the first code review pass, you want all the criticisms you can get. The more detailed the better, within limits.

- The code reviewer should be looking at many aspects of the code at once. The overall structure, the structure of individual methods or classes, the syntax, the nomenclature, the comments, the documentation, the testability, and the adherence to style guides used for your project. Checklists can help to make sure you don’t miss anything here.

- The commenters in a code review should start by trying to understand the motivation of the person writing the code. If that is not clear to you, then a good comment might be one inquiring as to the purpose of the code. Once you understand the coder’s motivation, use this perspective as a jumping off point to provide observations and suggestions that might make the code better. When critiquing someone else, starting from a perspective of understanding will help you to make a more informative and effective critique.

- Be clear, succinct, and courteous. This is the best way to make sure your critiques/comments are heard and understood. Give reasons to back up your suggestions. Cite style guides where they exist. Leave room for the other person to explain where you might be missing something.

- After the first round of comments, the person who requested the code review should review the comments and make changes or give feedback. Where in doubt, defer to the opinion of the reviewer. You can always change it later!

- Complete the code review soon after it was requested. Under 15 minutes is fantastic, under a day is great. Under a week can be fine depending on how the changes affect the project. Any longer than a week, and the changes begin to get stale. Not just in the codebase, but also in your head. The fresher you can be when reviewing the changes, the faster all the steps of the code review process will be. If the code begins to get old and stale, escalate the review of those changes in priority, or question whether they are important enough to matter in the first place.

- As a general comment on style, everything goes faster if pull requests are of a reasonable size. If the reviewer can grok your changes in under 5 minutes, you're golden. Sometimes a larger commit is necessary, and that's fine.

- However commits that take longer than 10-15 minutes to review should be questioned, or framed in a way that helps the reviewer understand why the commit must be so large. Larger commits slow project velocity due to this code review friction, and are to be avoided if possible.

- Notably, review of one’s own code prior to submission was shown to positively affect code quality as well.

- Where there are conflicts, bring in more reviewers and resolve outstanding questions. Don’t become attached to your code. Defer to the majority. And remember it can always change again later. ;)

And enjoy! Code review is one of the best opportunities to learn that you have on a daily basis. Take what you learn in code reviews and use that to improve your coding habits daily.

Happy coding!
