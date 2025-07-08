# Next.js: React's Glow-Up Era

### Ana Almonte

If you're comfortable with React, you're already 90% of the way to mastering Next.js. React gives you the power, but Next.js makes it easy to use like dropping a strong engine into a Porsche. It's fast, smooth and ready for the real world, with built-in features like routing, performance SEO (Search Engine Optimization) built in.

---

# Table of Contents

- [Why Next.js ?](#why-nextjs-)
- [The key differences](#the-key-differences)
- [How Next.js Handles What React Can't](#How-Next.js-Handles-What-React-Can't)
- [Set up](#set-up)
- [What stays the same](#what-stays-the-same)
- [My experience](#my-experience)
- [Should you switch?](#should-you-switch)
- [Getting started](#getting-started)

# Why Next.js ?

Companies like Netflix, TikTok, and Hulu chose Next.js over plain React for good reason. While React handles UI beautifully, Next.js handles everything else: routing, performance optimization, SEO, and deployment.

## How Next.js Handles What React Can't

**Routing**: In traditional React, you need to install and configure React Router, manually define routes, and manage navigation state. You have to wrap your app in `BrowserRouter`, define route components, and handle route parameters manually. Next.js makes this simple: create a file, get a route.

**SEO**: Traditional React apps are client-side rendered, meaning search engines see empty HTML until JavaScript loads. You'd need to set up server-side rendering manually using tools like Express.js and complex configurations. Next.js provides built-in SSR (Server-Side Rendering) SSG (Static Site Generation), so search engines receive fully rendered HTML content right away.

**Deployment**: With React, you need to build your app, configure a web server, handle routing on the server, and manage static file serving. Next.js simplifies this with platforms like Vercel, where deployment is as simple as connecting your Git repository.

# The key differences

**Basic React Router structure**:

```javascript
import { BrowserRouter, Routes, Route } from 'react-router-dom';

function App() {
return (
<BrowserRouter>
<Routes>
<Route path="/" element={<Home />} />
<Route path="/about" element={<About />} />
<Route path="/blog/:example" element={<BlogPost />} />
</Routes>
</BrowserRouter>
);
}
```

**Routing in Next.js**: Files instead of Code

```javascript
pages/
  index.js          // Homepage
  about.js          // /about page
  blog/
    [example].js       // /blog/anything
```

Create a file, get a route. That's it.

## How Next.js Makes This Work

When you create a file in the `pages` directory, Next.js automatically:
1. **Registers the route** - The file path becomes the URL path
2. **Code splits automatically** - Each page becomes its own JavaScript bundle
3. **Prefetches linked pages** - When a `Link` component is visible, Next.js prefetches that page's code
4. **Handles dynamic routing** - Files with brackets `[example].js` become dynamic routes that can accept parameters

No configuration needed, and you get performance benefits automatically.


# Set up

**React**:
```bash
npx create-react-app my-app
# Then install React Router
npm install react-router-dom
# Then configure react routing manually
# Then build for production
npm run build
# Then set up deployment
```

**Next.js**: zero configuration 
```bash
npx create-next-app my-app
npm run dev
```

You're done. Everything is handled for you.

# What stays the same

The React you know and love doesn't change. Components, hooks, state management. It all remains the same:

```javascript
import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

**This component works exactly the same in both React and Next.js.**

# My experience

While learning Next.js I built a mini Pinterest clone as a side project. Compared to using plain React, everything felt easier. Pages loaded faster, images were optimized automatically, and routing was built in.

## Building the PinCard Component

One specific example that showcased Next.js's advantages was building the PinCard component for displaying individual pins. In traditional React, I would have needed to:

```javascript
// Traditional React approach
import { useState, useEffect } from 'react';
import { useNavigate } from 'react-router-dom';

function PinCard({ pin }) {
  const [imageLoaded, setImageLoaded] = useState(false);
  const navigate = useNavigate();
  
  const handleClick = () => {
    navigate(`/pin/${pin.id}`);
  };
  
  return (
    <div onClick={handleClick} className="pin-card">
      <img 
        src={pin.image} 
        alt={pin.title}
        onLoad={() => setImageLoaded(true)}
        style={{ opacity: imageLoaded ? 1 : 0 }}
      />
      <h3>{pin.title}</h3>
    </div>
  );
}
```

With Next.js, the same component became much cleaner:

```javascript
// Next.js approach
import Image from 'next/image';
import Link from 'next/link';

function PinCard({ pin }) {
  return (
    <Link href={`/pin/${pin.id}`}>
      <div className="pin-card">
        <Image 
          src={pin.image} 
          alt={pin.title}
          width={300}
          height={400}
          placeholder="blur"
          blurDataURL="data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQ..."
        />
        <h3>{pin.title}</h3>
      </div>
    </Link>
  );
}
```

The Next.js version provided several advantages:
- **Automatic image optimization** - Images load faster and look better

- **Built-in lazy loading** - Images only load when you scroll to them
- **Prefetching** - Pages load before you click them
- **No routing state management** - The `Link` component handled navigation seamlessly

The Next.js documentation was incredibly helpful throughout this process. Unlike many frameworks, Next.js docs are practical and example driven, making it easy to understand not just what to do, but why certain patterns work better.

I did not deploy the project, but building with Next.js helped me understand how it simplifies a lot of setup and improves performance while also saving a lot of time.

**GitHub Repo:** [Mini-Pinterest](https://github.com/your-username/mini-pinterest)

# Should you switch?

If you're building more than just a basic project, then yes. Next.js is worth learning. It gives you powerful features like faster loading, better search engine optimization, and tools that make your app look more professional.

If you already know React, the learning curve is small. You're not starting over, you're just learning a better way to use what you already know.

# Getting started

```bash
npx create-next-app@latest my-project
cd my-project
npm run dev
```

I recommend you start with the [Next.js tutorial](https://nextjs.org/learn) (official Next.js site) - it's great and builds on React concepts you already understand.

**Next.js takes React to the next level. It doesn't replace React, it optimizes it.**

**Want to experience React's glow up? Try Next.js!**