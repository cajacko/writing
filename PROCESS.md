# Writing process

As an absolute nerd and dick I have written my writing process as a JavaScript function. Comments there for non programmers.

```typescript
// A variable that represents the current post I'm working on. Is set to null if I have no post on
let postInProgress: null | { topic: string; stage: number } = null;

// An ordered list of how I write a post
const postStages = [
  "Pick new post topic",
  "Write basic notes",
  "Creat a few ideation videos riffing off the notes",
  "Rewatch ideation videos and update notes",
  "Write the post",
  "Create a few videos communicating the idea, pick 1 final one"
];

// A function I go through in my head every time I sit down to work on a post
function onDailyWritingSession() {
  // A variable that gets set to false when I've done my time for the day
  let timeLeftInSession = true;

  // Whilst we still have time left to work, follow the logic inside this code block
  while (timeLeftInSession) {
    // If we hace a post in progress, work on it
    if (postInProgress) {
      // Work on the current stage of the post. Will run the specified item in the "postStages" array
      const finishedStage = workOnStage(postInProgress.stage);

      // If we finished the stage, then see if we've finished the post, otherwise set the next stage
      // We don't need to do anything more if we haven't finished this stage
      if (finishedStage) {
        // If we've finished the post, set postInProgress to null, so we know we need to select a new one
        if (hasFinishedPost(postInProgress)) {
          postInProgress = null;

          // We haven't finished the post, but have finished the stage, so indicate that we're moving onto the next stage
        } else {
          postInProgress.stage = postInProgress.stage + 1;
        }
      }

      // Setting this means we go through the while loop again if we have time left. Otherwise we leave it there
      timeLeftInSession = hasTimeLeftInSession();

      // Otherwise there is no post in progress, so pick one
    } else {
      const newPostTopic = pickNewPostTopic();

      postInProgress = {
        topic: newPostTopic,
        stage: 0
      };

      // We've set the new post, so let's go through this whole function again
      onDailyWritingSession();
    }
  }
}
```
