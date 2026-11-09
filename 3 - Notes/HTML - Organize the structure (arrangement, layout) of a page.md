Tags: [[__Frontend_engineering]] [[_HTML]]
#Frontend #HTML 

# Introduction
To organize the structure (arrangement, layout) of a page, we can use HTML elements such as:
- `<div>` - Generic block-level container
- `<span>` - Generic inline container
- `<section>` - Groups related content into a section
- `<article>` - Represents independent content, e.g. a blog post
- `<footer>` - Footer of a page/section (used for content at the bottom of a webpage or a section, e.g. copyright information, contact details, etc.)
- `<nav>` - Navigation links (that redirects to different pages or sections of a website)
- `<main>` - Main content of a page
- `<aside>` - Secondary or supplementary content

Example:
<body>
    <header>
        <h1>My Website</h1>
    </header>
    <nav>
        <a href="/">Home</a>
        <a href="/about">About</a>
    </nav>
    <main>
        <section>
            <h2>My Projects</h2>
            <article>
                <h3>Project 1</h3>
                <p>Project description...</p>
				<span>line item 1</span>
				<span>line item 2</span>
            </article>
        </section>
        <aside>
            Additional information
        </aside>
    </main>
    <footer>
        Copyright 2026
    </footer>
</body>
