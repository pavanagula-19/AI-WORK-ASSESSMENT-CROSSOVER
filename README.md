# AI-WORK-ASSESSMENT-CROSSOVER
Problem 1: Tags are broken up into individual characters on the post view page
Problem Statement:
When a user creates a new article with tags, the tags are displayed as individual characters on the post view page instead of as complete words.

Steps to Reproduce:

Log in to the application.
Create a new article with tags (e.g., coding, testing).
Submit the article.
Observe the tags on the post view page.
Root Cause:
The tags input was not being properly processed. Instead of splitting the tags by commas and trimming whitespace, the tags were being handled incorrectly, causing each character to be treated as a separate tag.

Solution:

Locate the code responsible for handling the tags during article creation in the frontend code (e.g., article-editor.component.ts).
Implement a function to split the tags by commas and trim whitespace.
Ensure this function is called when processing the tags input.
Code Changes:
In article-editor.component.ts:

// Function to split and trim tags
function processTags(tagString: string): string[] {
  return tagString.split(',').map(tag => tag.trim());
}

// Usage in the component
onSubmit() {
  const tags = processTags(this.articleForm.value.tagList);
  // Add the processed tags to the article object
  this.article.tagList = tags;
  // Proceed with article submission
}
Testing the Fix:

Save the changes and restart the frontend server if necessary.
Create a new article with tags (e.g., coding, testing).
Verify that the tags are displayed correctly on the post view page.
Problem 2: New tags are not shown on the home page under "Popular Tags"
Problem Statement:
When a user creates a new article with new tags, these tags do not appear in the "Popular Tags" section on the home page, even after refreshing the page.

Steps to Reproduce:

Log in to the application.
Create a new article with tags that do not yet exist (e.g., coding, testing).
Submit the article.
Refresh the home page.
Observe the "Popular Tags" section.
Root Cause:
The backend logic responsible for updating the popular tags was not correctly adding new tags to the database or updating the "Popular Tags" section.

Solution:

Locate the backend code responsible for handling article creation and tag updates (e.g., articles.js).
Implement a function to process and update the tags correctly.
Ensure this function is called when a new article is created.
Code Changes:
In articles.js:

// Backend route to update tags
router.post('/articles', async (req, res) => {
  const { tags } = req.body.article;
  const processedTags = processTags(tags);
  // Logic to save tags to the database and update popular tags
  // ...
});

// Function to split and trim tags
function processTags(tagString) {
  return tagString.split(',').map(tag => tag.trim());
}
Testing the Fix:

Save the changes and restart the backend server if necessary.
Create a new article with new tags (e.g., coding, testing).
Refresh the home page.
Verify that the new tags appear in the "Popular Tags" section.
Acceptance Test
Log In:

Use the provided credentials to log in.
Create a New Article:

Create a new article with the tags coding, testing.
Verify:

Refresh the page and open the global feed.
Ensure that both tags are visible for your post and in the "Popular Tags" section.
