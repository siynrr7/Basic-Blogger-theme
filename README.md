# Basic-Blogger-theme
.
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE html>
<html b:css='false' b:defaultwidgetversion='2' b:layoutsversion='3' expr:dir='data:blog.languageDirection' xmlns='http://www.w3.org/1999/xhtml' xmlns:b='http://www.google.com/2005/gml/b' xmlns:data='http://www.google.com/2005/gml/data' xmlns:expr='http://www.google.com/2005/gml/expr'>
<head>
    <meta charset='utf-8'/>
    <meta content='width=device-width, initial-scale=1' name='viewport'/>
    <title><data:blog.pageTitle/></title>
    
    <b:include data='blog' name='all-head-content'/>

    <style>
        :root {
            --bg: #ffffff;
            --surface: #f8fafc;
            --text: #1e293b;
            --text-light: #64748b;
            --primary: #2563eb;
            --border: #e2e8f0;
            --code-bg: #1e293b;
            --code-text: #f8fafc;
            --max-width: 1000px;
        }

        @media (prefers-color-scheme: dark) {
            :root {
                --bg: #0f172a;
                --surface: #1e293b;
                --text: #f1f5f9;
                --text-light: #94a3b8;
                --primary: #60a5fa;
                --border: #334155;
            }
        }

        * { box-sizing: border-box; }
        body {
            font-family: ui-sans-serif, system-ui, -apple-system, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            line-height: 1.6;
            margin: 0;
            -webkit-font-smoothing: antialiased;
        }

        a { color: var(--primary); text-decoration: none; }
        a:hover { text-decoration: underline; }

        .container {
            max-width: var(--max-width);
            margin: 0 auto;
            padding: 0 1.5rem;
        }

        /* Header */
        header {
            border-bottom: 1px solid var(--border);
            padding: 1rem 0;
            background: var(--bg);
            position: sticky;
            top: 0;
            z-index: 10;
        }

        .nav-wrapper {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo { font-weight: 700; font-size: 1.25rem; }

        nav ul { display: flex; list-style: none; gap: 1.5rem; margin: 0; padding: 0; }
        nav a { color: var(--text); font-weight: 500; font-size: 0.9rem; }

        /* Main Layout */
        .main-grid {
            display: grid;
            grid-template-columns: 1fr 300px;
            gap: 3rem;
            margin: 3rem 0;
        }

        @media (max-width: 850px) {
            .main-grid { grid-template-columns: 1fr; }
            aside { display: none; }
        }

        /* Post Styles */
        article { margin-bottom: 3rem; }
        .post-meta { font-size: 0.85rem; color: var(--text-light); margin-bottom: 0.5rem; }
        .post-title { font-size: 2rem; margin: 0 0 1rem; line-height: 1.2; }
        .post-title a { color: var(--text); }
        .post-body { font-size: 1.05rem; }
        .post-body img { max-width: 100%; border-radius: 8px; height: auto; }

        /* Tool Card (Microblog variant) */
        .microblog {
            background: var(--surface);
            padding: 1.5rem;
            border-radius: 12px;
            border: 1px solid var(--border);
        }

        /* Pagination */
        .pagination {
            display: flex;
            justify-content: space-between;
            padding: 2rem 0;
            border-top: 1px solid var(--border);
        }

        .btn {
            padding: 0.6rem 1.2rem;
            border-radius: 6px;
            border: 1px solid var(--border);
            background: var(--surface);
            font-size: 0.9rem;
            font-weight: 600;
        }

        /* Sidebar Widgets */
        .widget { margin-bottom: 2.5rem; }
        .widget h2 { font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.05em; color: var(--text-light); margin-bottom: 1rem; }
        .widget ul { list-style: none; padding: 0; margin: 0; }
        .widget li { margin-bottom: 0.5rem; }

        footer {
            text-align: center;
            padding: 4rem 0;
            color: var(--text-light);
            font-size: 0.9rem;
            border-top: 1px solid var(--border);
        }

        /* Blogger Specific Fixes */
        .status-msg-wrap { display: none; }
    </style>

    <b:skin><![CDATA[
        /* Required for Blogger UI */
    ]]></b:skin>
</head>

<body>
    <header>
        <div class='container nav-wrapper'>
            <div class='logo'>
                <a expr:href='data:blog.homepageUrl'><data:blog.title/></a>
            </div>
            <b:section id='nav-menu' maxwidgets='1' showaddelement='no'>
                <b:widget id='PageList1' locked='true' title='Menu' type='PageList'>
                    <b:includable id='main'>
                        <nav>
                            <ul>
                                <b:loop values='data:links' var='link'>
                                    <li><a expr:href='data:link.href'><data:link.title/></a></li>
                                </b:loop>
                            </ul>
                        </nav>
                    </b:includable>
                </b:widget>
            </b:section>
        </div>
    </header>

    <main class='container main-grid'>
        <div class='content-area'>
            <b:section id='main' showaddelement='no'>
                <b:widget id='Blog1' locked='true' title='Posts' type='Blog'>
                    <b:includable id='main'>
                        <b:loop values='data:posts' var='post'>
                            <b:include data='post' name='postContent'/>
                        </b:loop>
                        <b:include name='nextprev'/>
                    </b:includable>

                    <b:includable id='postContent' var='post'>
                        <article expr:class='data:post.labels any (l =&gt; l.name == "Post") ? "microblog" : ""'>
                            <div class='post-meta'>
                                <data:post.timestamp/>
                                <b:if cond='data:post.labels'>
                                    in <b:loop values='data:post.labels' var='label'>
                                        <a expr:href='data:label.url' rel='tag'><data:label.name/></a><b:if cond='not data:label.isLast'>, </b:if>
                                    </b:loop>
                                </b:if>
                            </div>

                            <b:if cond='data:post.title'>
                                <h2 class='post-title'>
                                    <b:if cond='data:post.link or (data:post.url and data:blog.url != data:post.url)'>
                                        <a expr:href='data:post.link ? data:post.link : data:post.url'><data:post.title/></a>
                                    <b:else/>
                                        <data:post.title/>
                                    </b:if>
                                </h2>
                            </b:if>

                            <div class='post-body'>
                                <data:post.body/>
                            </div>
                        </article>
                    </b:includable>

                    <b:includable id='nextprev'>
                        <div class='pagination'>
                            <b:if cond='data:newerPageUrl'>
                                <a class='btn' expr:href='data:newerPageUrl'>&amp;larr; Newer</a>
                            </b:if>
                            <b:if cond='data:olderPageUrl'>
                                <a class='btn' expr:href='data:olderPageUrl'>Older &amp;rarr;</a>
                            </b:if>
                        </div>
                    </b:includable>
                </b:widget>
            </b:section>
        </div>

        <aside>
            <b:section id='sidebar' preferred='yes'>
                <b:widget id='Label1' locked='false' title='Categories' type='Label'/>
            </b:section>
        </aside>
    </main>

    <footer>
        <div class='container'>
            &amp;copy; <span id='year'/> <data:blog.title/>. Built for performance.
        </div>
    </footer>

    <script>
        document.getElementById('year').textContent = new Date().getFullYear();
        
        // Performance: Lazy load image observer
        document.addEventListener("DOMContentLoaded", () => {
            const imgs = document.querySelectorAll('img');
            imgs.forEach(img => {
                if(!img.getAttribute('loading')) img.setAttribute('loading', 'lazy');
            });
        });
    </script>
</body>
</html>
