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

## Next.js

### App vs Pages Router

**Installing with Pages router:**

```shell
npx makeswift@latest init --template basic-typescript-pages
```