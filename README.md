

# Rendering GitHub Flavored Markdown in a Next.js App

This guide will help you set up a Next.js project to render GitHub Flavored Markdown (GFM) using `react-markdown` and `remark-gfm`. You'll also learn how to style your Markdown content with custom CSS.

## Step-by-Step Guide

### Step 1: Set Up a Next.js Project

If you haven't already, create a new Next.js project using `create-next-app`.

```sh
npx create-next-app@latest my-nextjs-markdown-app
cd my-nextjs-markdown-app
```

### Step 2: Install Necessary Libraries

- `react-markdown` for rendering Markdown content.
- `remark-gfm` for GitHub Flavored Markdown (GFM) support.

```sh
npm install react-markdown remark-gfm
```

### Step 3: Create a Markdown Component

Create a component to handle Markdown rendering.

```jsx
// components/Markdown.js
import React from 'react';
import ReactMarkdown from 'react-markdown';
import remarkGfm from 'remark-gfm';

const Markdown = ({ content }) => {
  return (
    <ReactMarkdown remarkPlugins={[remarkGfm]}>
      {content}
    </ReactMarkdown>
  );
};

export default Markdown;
```

### Step 4: Use the Markdown Component in a Page

Import and use the `Markdown` component in your Next.js page.

```jsx
// pages/index.js
import React from 'react';
import Markdown from '../components/Markdown';

const markdownContent = `
# Hello World

This is a **Next.js** app with GitHub Flavored Markdown support.

- List item 1
- List item 2

\`\`\`javascript
console.log('Hello, world!');
\`\`\`
`;

const Home = () => {
  return (
    <div>
      <h1>Next.js Markdown Example</h1>
      <Markdown content={markdownContent} />
    </div>
  );
};

export default Home;
```

### Step 5: Run Your Next.js App

Start your Next.js development server to see the Markdown rendering in action.

```sh
npm run dev
```

Now, when you navigate to the home page of your Next.js app, you should see the rendered Markdown content.

## Additional Features

### Syntax Highlighting

If you need syntax highlighting for code blocks, you can use `rehype-highlight`.

#### Install `rehype-highlight`

```sh
npm install rehype-highlight
```

#### Update the Markdown Component

```jsx
// components/Markdown.js
import React from 'react';
import ReactMarkdown from 'react-markdown';
import remarkGfm from 'remark-gfm';
import rehypeHighlight from 'rehype-highlight';
import 'highlight.js/styles/github.css'; // Import a highlight.js theme

const Markdown = ({ content }) => {
  return (
    <ReactMarkdown
      remarkPlugins={[remarkGfm]}
      rehypePlugins={[rehypeHighlight]}
    >
      {content}
    </ReactMarkdown>
  );
};

export default Markdown;
```

### Custom CSS Styling

Sometimes, the default styling may not be applied correctly. Add some CSS to style the Markdown elements.

#### Create a CSS File

```css
/* styles/markdown.css */

/* General */
.markdown {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  color: #333;
}

/* Headings */
.markdown h1 {
  font-size: 2.5em;
  margin-top: 1em;
  margin-bottom: 0.5em;
  border-bottom: 2px solid #eaecef;
  padding-bottom: 0.3em;
}

.markdown h2 {
  font-size: 2em;
  margin-top: 1em;
  margin-bottom: 0.5em;
  border-bottom: 1px solid #eaecef;
  padding-bottom: 0.3em;
}

.markdown h3 {
  font-size: 1.75em;
  margin-top: 1em;
  margin-bottom: 0.5em;
}

.markdown h4 {
  font-size: 1.5em;
  margin-top: 1em;
  margin-bottom: 0.5em;
}

.markdown h5 {
  font-size: 1.25em;
  margin-top: 1em;
  margin-bottom: 0.5em;
}

.markdown h6 {
  font-size: 1em;
  margin-top: 1em;
  margin-bottom: 0.5em;
  color: #777;
}

/* Paragraphs */
.markdown p {
  margin: 0.5em 0;
}

/* Lists */
.markdown ul {
  list-style-type: disc;
  padding-left: 40px;
  margin: 0.5em 0;
}

.markdown ol {
  list-style-type: decimal;
  padding-left: 40px;
  margin: 0.5em 0;
}

.markdown li {
  margin-bottom: 0.5em;
}

/* Code Blocks */
.markdown pre {
  background: #f6f8fa;
  padding: 1em;
  border-radius: 5px;
  overflow-x: auto;
  margin: 0.5em 0;
}

.markdown code {
  background: #f6f8fa;
  padding: 0.2em 0.4em;
  border-radius: 3px;
}

/* Blockquotes */
.markdown blockquote {
  padding: 0.5em 1em;
  margin: 0.8em 0;
  border-left: 4px solid #dfe2e5;
  color: #6a737d;
  background: #f6f8fa;
}

/* Tables */
.markdown table {
  width: 100%;
  border-collapse: collapse;
  margin: 1em 0;
}

.markdown th,
.markdown td {
  padding: 0.6em 1em;
  border: 1px solid #dfe2e5;
}

.markdown th {
  background: #f6f8fa;
  font-weight: bold;
}

.markdown td {
  background: #fff;
}

/* Links */
.markdown a {
  color: #0366d6;
  text-decoration: none;
}

.markdown a:hover {
  text-decoration: underline;
}

/* Horizontal Rules */
.markdown hr {
  border: 0;
  border-top: 1px solid #dfe2e5;
  margin: 1em 0;
}
```

#### Apply CSS Styling

Import the CSS file into your Markdown component.

```jsx
// components/Markdown.js
import React from 'react';
import ReactMarkdown from 'react-markdown';
import remarkGfm from 'remark-gfm';
import rehypeHighlight from 'rehype-highlight';
import 'highlight.js/styles/github.css'; // Import a highlight.js theme
import '../styles/markdown.css'; // Import custom styles

const Markdown = ({ content }) => {
  return (
    <div className="markdown">
      <ReactMarkdown
        remarkPlugins={[remarkGfm]}
        rehypePlugins={[rehypeHighlight]}
      >
        {content}
      </ReactMarkdown>
    </div>
  );
};

export default Markdown;
```

### Sample Markdown Content

You can test the styles with the following sample Markdown content.

```jsx
// pages/index.js
import React from 'react';
import Markdown from '../components/Markdown';

const markdownContent = `
# Heading 1

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6

This is a paragraph with **bold** text, *italic* text, and [a link](https://example.com).

- Unordered list item 1
- Unordered list item 2
  - Nested list item
  - Another nested item

1. Ordered list item 1
2. Ordered list item 2
   1. Nested ordered item
   2. Another nested item

\`\`\`javascript
console.log('Code block');
\`\`\`

\`Inline code\`

> This is a blockquote.

---

| Header 1 | Header 2 |
| -------- | -------- |
| Cell 1   | Cell 2   |
| Cell 3   | Cell 4   |
`;

const Home = () => {
  return (
    <div>
      <h1>Next.js Markdown Example</h1>
      <Markdown content={markdownContent} />
    </div>
  );
};

export default Home;
