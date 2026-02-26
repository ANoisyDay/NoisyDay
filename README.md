# NoisyDay
We started creating films together in our early college years and have learned narrative in any form is essential. On Noisy Day we strive to tell original stories, wether that’s documentary’s, commercial’s, or films. 
# Noisy Day — Webflow Build Plan
1) package.json
{
  "name": "noisy-day",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev -p 3000",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "clsx": "^1.2.1",
    "next": "13.4.10",
    "react": "18.2.0",
    "react-dom": "18.2.0",
    "tailwindcss": "^3.5.0",
    "autoprefixer": "^10.4.0",
    "postcss": "^8.4.0"
  }
}
2) next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  images: {
    remotePatterns: [
      { protocol: 'https', hostname: 'images.unsplash.com' },
      { protocol: 'https', hostname: 'cdn.shopify.com' }
    ]
  }
};

module.exports = nextConfig;

3) tailwind.config.js
module.exports = {
  content: ['./pages/**/*.{js,jsx}', './components/**/*.{js,jsx}'],
  theme: {
    extend: {
      colors: {
        primary: '#111827',
        accent: '#e11d48'
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif']
      }
    }
  },
  plugins: []

4) postcss.config.js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {}
  }
};

5) styles/globals.css
@tailwind base;
@tailwind components;
@tailwind utilities;

html, body, #__next { height: 100%; }

body {
  @apply bg-white text-gray-900 antialiased;
  font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
}

.container {
  max-width: 1100px;
  margin-left: auto;
  margin-right: auto;
  padding-left: 16px;
  padding-right: 16px;
}

/* utility for card shadows used sparingly */
.card {
  @apply border border-gray-200 rounded;
}

6) data/articles.js (seed content)
export const articles = [
  {
    slug: 'how-the-city-sounds',
    title: 'How the City Sounds',
    excerpt: 'On listening to the city and why small noises tell big stories.',
    cover: 'https://images.unsplash.com/photo-1507525428034-b723cf961d3e?w=1200&q=80&auto=format&fit=crop',
    content: '<p>This is demo article content for Noisy Day. Replace with your CMS content or extend this file.</p>',
    date: '2026-02-01',
    vertical: 'Noisy Day'
  },
  {
    slug: 'field-recordings-from-the-street',
    title: 'Field Recordings From the Street',
    excerpt: 'An experiment in urban listening — Field Day highlights.',
    cover: 'https://images.unsplash.com/photo-1519681393784-d120267933ba?w=1200&q=80&auto=format&fit=crop',
    content: '<p>Field Day piece: local sounds and interviews.</p>',
    date: '2026-01-28',
    vertical: 'Field Day'
  },
  {
    slug: 'small-venues-big-noise',
    title: 'Small Venues, Big Noise',
    excerpt: 'How local spots keep culture alive.',
    cover: 'https://images.unsplash.com/photo-1515586322730-6d50b1b47c79?w=1200&q=80&auto=format&fit=crop',
    content: '<p>Story on small clubs and soundscapes.</p>',
    date: '2026-01-12',
    vertical: 'Noisy Day'
  }
];

7) data/products.js (seed shop)

export const products = [
  {
    id: 'noisy-hoodie',
    title: 'Noisy Day Hoodie',
    price: 60,
    image: 'https://images.unsplash.com/photo-1512436991641-6745cdb1723f?w=800&q=80&auto=format&fit=crop'
  },
  {
    id: 'noisy-sticker',
    title: 'Noisy Day Sticker',
    price: 5,
    image: 'https://images.unsplash.com/photo-1526312477-0f2a0a7e6e2b?w=800&q=80&auto=format&fit=crop'
  }
];

8) components/SEO.js

import Head from 'next/head';

export default function SEO({ title, description, image }) {
  return (
    <Head>
      <title>{title ? `${title} — Noisy Day` : 'Noisy Day'}</title>
      <meta name="description" content={description || 'Noisy Day — editorial on sound and culture.'} />
      <meta property="og:title" content={title ? `${title} — Noisy Day` : 'Noisy Day'} />
      <meta property="og:description" content={description || 'Noisy Day — editorial on sound and culture.'} />
      {image && <meta property="og:image" content={image} />}
      <meta name="twitter:card" content="summary_large_image" />
    </Head>
  );
}

9) components/Header.js

import Link from 'next/link';

export default function Header() {
  return (
    <header className="border-b">
      <div className="container flex items-center justify-between py-4">
        <div>
          <Link href="/"><a className="text-2xl font-bold">Noisy Day</a></Link>
        </div>
        <nav className="space-x-6 text-sm">
          <Link href="/"><a>Home</a></Link>
          <Link href="/field-day"><a>Field Day</a></Link>
          <Link href="/shop"><a>Shop</a></Link>
          <Link href="/about"><a>About</a></Link>
        </nav>
      </div>
    </header>
  );
}

10) components/Footer.js

export default function Footer() {
  return (
    <footer className="border-t mt-12 py-8">
      <div className="container text-sm text-gray-600">
        © {new Date().getFullYear()} Noisy Day. Made with sound.
      </div>
    </footer>
  );
}

11) components/Hero.js

export default function Hero({ title, subtitle }) {
  return (
    <section className="py-12">
      <div className="container">
        <h1 className="text-4xl md:text-5xl font-extrabold leading-tight">{title}</h1>
        {subtitle && <p className="mt-4 text-lg text-gray-700">{subtitle}</p>}
      </div>
    </section>
  );
}

12) components/ArticleCard.js

import Link from 'next/link';
import Image from 'next/image';

export default function ArticleCard({ article }) {
  return (
    <article className="group card overflow-hidden">
      <Link href={`/articles/${article.slug}`}>
        <a className="block">
          <div className="relative h-56">
            <Image src={article.cover} alt={article.title} fill style={{objectFit:'cover'}} sizes="(max-width:768px) 100vw, 33vw" />
          </div>
          <div className="p-4">
            <h3 className="text-xl font-semibold group-hover:underline">{article.title}</h3>
            <p className="text-sm text-gray-600 mt-2">{article.excerpt}</p>
            <p className="text-xs text-gray-400 mt-2">{article.date} · {article.vertical}</p>
          </div>
        </a>
      </Link>
    </article>
  );
}

13) components/ShopCard.js

export default function ShopCard({ product }) {
  return (
    <div className="card p-4">
      <img src={product.image} alt={product.title} className="w-full h-48 object-cover rounded" />
      <h4 className="mt-3 font-semibold">{product.title}</h4>
      <div className="mt-2 flex items-center justify-between">
        <span className="font-medium">${product.price}</span>
        <button className="px-3 py-1 border rounded">Buy</button>
      </div>
    </div>
  );
}

14) components/SocialEmbed.js (lazy YouTube)

export default function SocialEmbed({ videoId }) {
  return (
    <div className="yt-lite relative w-full" style={{paddingTop: '56.25%'}} data-id={videoId}>
      <div className="absolute inset-0 cursor-pointer" onClick={(e)=>{
        const parent = e.currentTarget.parentNode;
        const id = parent.dataset.id;
        const iframe = document.createElement('iframe');
        iframe.src = `https://www.youtube.com/embed/${id}?autoplay=1&rel=0`;
        iframe.allow = 'accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture';
        iframe.frameBorder = '0';
        iframe.style.width = '100%';
        iframe.style.height = '100%';
        parent.replaceWith(iframe);
      }} />
      <style jsx>{`
        .yt-lite { background-size: cover; background-position: center; }
      `}</style>
    </div>
  );
}

15) pages/_app.js

import '../styles/globals.css';

export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />;
}

16) pages/index.js (home + Field Day landing logic)

import Header from '../components/Header';
import Footer from '../components/Footer';
import Hero from '../components/Hero';
import ArticleCard from '../components/ArticleCard';
import SEO from '../components/SEO';
import { articles } from '../data/articles';
import Link from 'next/link';

export default function Home({ filter }) {
  // query param filter decides vertical. But since this is static, we'll rely on paths.
  const pathname = typeof window !== 'undefined' ? window.location.pathname : '';
  const isFieldDay = pathname.includes('field-day') || filter === 'Field Day';
  const list = articles.filter(a => !isFieldDay || a.vertical === 'Field Day');

  return (
    <>
      <SEO title="Noisy Day" description="Noisy Day — editorial on sounds and culture" />
      <Header />
      <main>
        <Hero title="Noisy Day" subtitle="Stories, field recordings, and conversations about sound." />
        <div className="container grid grid-cols-1 md:grid-cols-3 gap-6">
          {list.map(a => <ArticleCard key={a.slug} article={a} />)}
        </div>

        <section className="container mt-12">
          <div className="flex items-center justify-between">
            <h2 className="text-xl font-semibold">Shop</h2>
            <Link href="/shop"><a className="text-sm">See all</a></Link>
          </div>
          {/* show 2 products as teaser */}
        </section>
      </main>
      <Footer />
    </>
  );
}

17) pages/articles/[slug].js

import { useRouter } from 'next/router';
import Header from '../../components/Header';
import Footer from '../../components/Footer';
import SEO from '../../components/SEO';
import Image from 'next/image';
import { articles } from '../../data/articles';

export default function ArticlePage() {
  const router = useRouter();
  const { slug } = router.query;
  const article = articles.find(a => a.slug === slug);

  if (!article) {
    return (
      <>
        <Header />
        <div className="container py-12">Loading…</div>
        <Footer />
      </>
    );
  }

  return (
    <>
      <SEO title={article.title} description={article.excerpt} image={article.cover} />
      <Header />
      <main className="container py-8">
        <h1 className="text-3xl font-bold">{article.title}</h1>
        <p className="text-sm text-gray-500 mt-2">{article.date} · {article.vertical}</p>
        <div className="relative w-full h-72 my-4">
          <Image src={article.cover} alt={article.title} fill style={{objectFit:'cover'}} />
        </div>
        <article className="prose" dangerouslySetInnerHTML={{ __html: article.content }} />
      </main>
      <Footer />
    </>
  );
}

18) pages/shop.js

import Header from '../components/Header';
import Footer from '../components/Footer';
import ShopCard from '../components/ShopCard';
import { products } from '../data/products';

export default function Shop() {
  return (
    <>
      <Header />
      <main className="container py-8">
        <h1 className="text-2xl font-bold">Shop</h1>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6 mt-6">
          {products.map(p => <ShopCard key={p.id} product={p} />)}
        </div>
      </main>
      <Footer />
    </>
  );
}

19) pages/field-day.js (dedicated Field Day landing)

import Home from './index';
import { articles } from '../data/articles';

export default function FieldDay() {
  // render the Home component but filtered to Field Day
  return <Home filter="Field Day" articles={articles} />;
}

20) public/favicon.ico

21) README.md (local + GitHub instructions)

# Noisy Day — Next.js + Tailwind starter

## Run locally
1. Install deps:

npm install

2. Start dev server:

npm run dev

3. Open http://localhost:3000

## Deploy to Vercel
1. Create a GitHub repo and push this project (commands below).
2. Sign in to vercel.com and *Import Project* => pick the GitHub repo and deploy.

## Git commands to create repo and push
```bash
git init
git add .
git commit -m "Initial commit - Noisy Day starter"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/noisy-day.git
git push -u origin main


---

## Legal & ethical note
This starter is an original implementation inspired by the publicopinion.nyc site architecture and visual approach. Do **not** copy text, images, or proprietary content from the original site without permission. Use this repo as a starting point and replace seed content with your own.

---

## Next steps I can do right now (pick any)
- Convert this into a ZIP and give you a ready-to-upload package (I can paste full files again for direct copy).  
- Add `getStaticProps` / `getStaticPaths` so pages are pre-rendered (good for SEO) — I’ll wire it to the local `data/` files.  
- Replace the Shop `Buy` buttons with a Shopify Buy Button snippet or Snipcart integration.  
- Create a simple logo image and color palette for Noisy Day and Field Day.

Which of these would you like next? If you want, I’ll **also** paste the exact `git` commands again and create the branch structure you can push.




