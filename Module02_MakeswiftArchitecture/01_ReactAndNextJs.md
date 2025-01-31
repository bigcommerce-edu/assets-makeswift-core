# React and Next.js

## React

**React Example:**

```javascript
const BlogList = ({
  title,
  articles
}) => {
  const onLikeClick = async (id) => {
    await fetch("/likeArticle", {
      method: "POST",
      body: JSON.stringify({ id });
    });
  };

  return (
    <div>
      <h1>{title}</h1>
      <ul>
        {articles.map(article => (
          <li><a href="{article.url}">
            <h2>{article.title}</h2>
            <div>{article.summary}</div>
            <button onClick={() => onLikeClick(article.id)}>Like</button>
          </a></li>
        )}
      </ul>
    </div>
  );
}
```

[Next](../Module03_CustomComponents/01_MakeswiftComponentApproach.md)
