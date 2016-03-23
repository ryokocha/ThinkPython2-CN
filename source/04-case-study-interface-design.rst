



<!DOCTYPE html>
<html lang="en" class=" is-copy-enabled is-u2f-enabled">
  <head prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb# object: http://ogp.me/ns/object# article: http://ogp.me/ns/article# profile: http://ogp.me/ns/profile#">
    <meta charset='utf-8'>

    <link crossorigin="anonymous" href="https://assets-cdn.github.com/assets/frameworks-dc6f99c21c664327b3323c443396ffc273e4005a7660629ebf8b359a46459647.css" integrity="sha256-3G+ZwhxmQyezMjxEM5b/wnPkAFp2YGKev4s1mkZFlkc=" media="all" rel="stylesheet" />
    <link crossorigin="anonymous" href="https://assets-cdn.github.com/assets/github-d6cdc916c67f2afd181c5dd292db1fdb3e93fc18d67b4a8cdac0ef77df6b9cc9.css" integrity="sha256-1s3JFsZ/Kv0YHF3Sktsf2z6T/BjWe0qM2sDvd99rnMk=" media="all" rel="stylesheet" />
    
    
    
    

    <link as="script" href="https://assets-cdn.github.com/assets/frameworks-20e2831691c9bb0a4dc1bd778529fc1c16ec8c8a24b32d9964f984772d2eb24b.js" rel="preload" />
    <link as="script" href="https://assets-cdn.github.com/assets/github-ab1086948a3be528001710080ba17e4975ddb36a9379ab7dddfdb0370647b7c1.js" rel="preload" />

    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta http-equiv="Content-Language" content="en">
    <meta name="viewport" content="width=1020">
    
    
    <title>ThinkPython2-CN/04-case-study-interface-design.rst at master · bingjin/ThinkPython2-CN</title>
    <link rel="search" type="application/opensearchdescription+xml" href="/opensearch.xml" title="GitHub">
    <link rel="fluid-icon" href="https://github.com/fluidicon.png" title="GitHub">
    <link rel="apple-touch-icon" href="/apple-touch-icon.png">
    <link rel="apple-touch-icon" sizes="57x57" href="/apple-touch-icon-57x57.png">
    <link rel="apple-touch-icon" sizes="60x60" href="/apple-touch-icon-60x60.png">
    <link rel="apple-touch-icon" sizes="72x72" href="/apple-touch-icon-72x72.png">
    <link rel="apple-touch-icon" sizes="76x76" href="/apple-touch-icon-76x76.png">
    <link rel="apple-touch-icon" sizes="114x114" href="/apple-touch-icon-114x114.png">
    <link rel="apple-touch-icon" sizes="120x120" href="/apple-touch-icon-120x120.png">
    <link rel="apple-touch-icon" sizes="144x144" href="/apple-touch-icon-144x144.png">
    <link rel="apple-touch-icon" sizes="152x152" href="/apple-touch-icon-152x152.png">
    <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon-180x180.png">
    <meta property="fb:app_id" content="1401488693436528">

      <meta content="https://avatars0.githubusercontent.com/u/14083704?v=3&amp;s=400" name="twitter:image:src" /><meta content="@github" name="twitter:site" /><meta content="summary" name="twitter:card" /><meta content="bingjin/ThinkPython2-CN" name="twitter:title" /><meta content="ThinkPython2-CN - 《Think Python 2ed》最新版中文翻译，持续更新中。" name="twitter:description" />
      <meta content="https://avatars0.githubusercontent.com/u/14083704?v=3&amp;s=400" property="og:image" /><meta content="GitHub" property="og:site_name" /><meta content="object" property="og:type" /><meta content="bingjin/ThinkPython2-CN" property="og:title" /><meta content="https://github.com/bingjin/ThinkPython2-CN" property="og:url" /><meta content="ThinkPython2-CN - 《Think Python 2ed》最新版中文翻译，持续更新中。" property="og:description" />
      <meta name="browser-stats-url" content="https://api.github.com/_private/browser/stats">
    <meta name="browser-errors-url" content="https://api.github.com/_private/browser/errors">
    <link rel="assets" href="https://assets-cdn.github.com/">
    <link rel="web-socket" href="wss://live.github.com/_sockets/NjU2ODg5NTpjNDNhYWFiMWY0NDhmMWMyZmY4ZjllZjVlNTU4NzlkYTpiMGRlZWE1ZWU4YjcyMDEyNDZhOTBhNzU4NzY5OGVjOWM4YTU2ZTdjZDRjZjZjMzA0ZDllNTczMTRmYmNkNmVl--e249ce9c9e92838aafcf330c373e4ed58ff1a228">
    <meta name="pjax-timeout" content="1000">
    <link rel="sudo-modal" href="/sessions/sudo_modal">

    <meta name="msapplication-TileImage" content="/windows-tile.png">
    <meta name="msapplication-TileColor" content="#ffffff">
    <meta name="selected-link" value="repo_source" data-pjax-transient>

    <meta name="google-site-verification" content="KT5gs8h0wvaagLKAVWq8bbeNwnZZK1r1XQysX3xurLU">
<meta name="google-site-verification" content="ZzhVyEFwb7w3e0-uOTltm8Jsck2F5StVihD0exw2fsA">
    <meta name="google-analytics" content="UA-3769691-2">

<meta content="collector.githubapp.com" name="octolytics-host" /><meta content="github" name="octolytics-app-id" /><meta content="DDE2058C:38FD:10664AFB:56F23D61" name="octolytics-dimension-request_id" /><meta content="6568895" name="octolytics-actor-id" /><meta content="SeikaScarlet" name="octolytics-actor-login" /><meta content="dad84e9193072c368393cb4c47f3a3703d2fd1b79f25e742372045ffbc5e083d" name="octolytics-actor-hash" />
<meta content="/&lt;user-name&gt;/&lt;repo-name&gt;/blob/show" data-pjax-transient="true" name="analytics-location" />



  <meta class="js-ga-set" name="dimension1" content="Logged In">



        <meta name="hostname" content="github.com">
    <meta name="user-login" content="SeikaScarlet">

        <meta name="expected-hostname" content="github.com">
      <meta name="js-proxy-site-detection-payload" content="NzNlZmRjMTRhNGQzOGRlZDgxMTZiZDE2ODg4ZjE4NmExNWQwYzE3ZDFiZjg1ZjgyMTM3NjZmNDZiNTZkMThiOHx7InJlbW90ZV9hZGRyZXNzIjoiMjIxLjIyNi41LjE0MCIsInJlcXVlc3RfaWQiOiJEREUyMDU4QzozOEZEOjEwNjY0QUZCOjU2RjIzRDYxIn0=">

      <link rel="mask-icon" href="https://assets-cdn.github.com/pinned-octocat.svg" color="#4078c0">
      <link rel="icon" type="image/x-icon" href="https://assets-cdn.github.com/favicon.ico">

    <meta content="781ac8e9c6c1aaed08e5802cfa0e40bddd06cdfb" name="form-nonce" />

    <meta http-equiv="x-pjax-version" content="1e238f7ce64eca26eae976d60aa3230c">
    

      
  <meta name="description" content="ThinkPython2-CN - 《Think Python 2ed》最新版中文翻译，持续更新中。">
  <meta name="go-import" content="github.com/bingjin/ThinkPython2-CN git https://github.com/bingjin/ThinkPython2-CN.git">

  <meta content="14083704" name="octolytics-dimension-user_id" /><meta content="bingjin" name="octolytics-dimension-user_login" /><meta content="52792140" name="octolytics-dimension-repository_id" /><meta content="bingjin/ThinkPython2-CN" name="octolytics-dimension-repository_nwo" /><meta content="true" name="octolytics-dimension-repository_public" /><meta content="false" name="octolytics-dimension-repository_is_fork" /><meta content="52792140" name="octolytics-dimension-repository_network_root_id" /><meta content="bingjin/ThinkPython2-CN" name="octolytics-dimension-repository_network_root_nwo" />
  <link href="https://github.com/bingjin/ThinkPython2-CN/commits/master.atom" rel="alternate" title="Recent Commits to ThinkPython2-CN:master" type="application/atom+xml">


      <link rel="canonical" href="https://github.com/bingjin/ThinkPython2-CN/blob/master/source/04-case-study-interface-design.rst" data-pjax-transient>
  </head>


  <body class="logged-in   env-production windows vis-public page-blob">
    <div id="js-pjax-loader-bar" class="pjax-loader-bar"></div>
    <a href="#start-of-content" tabindex="1" class="accessibility-aid js-skip-to-content">Skip to content</a>

    
    
    



        <div class="header header-logged-in true" role="banner">
  <div class="container clearfix">

    <a class="header-logo-invertocat" href="https://github.com/" data-hotkey="g d" aria-label="Homepage" data-ga-click="Header, go to dashboard, icon:logo">
  <svg aria-hidden="true" class="octicon octicon-mark-github" height="28" role="img" version="1.1" viewBox="0 0 16 16" width="28"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59 0.4 0.07 0.55-0.17 0.55-0.38 0-0.19-0.01-0.82-0.01-1.49-2.01 0.37-2.53-0.49-2.69-0.94-0.09-0.23-0.48-0.94-0.82-1.13-0.28-0.15-0.68-0.52-0.01-0.53 0.63-0.01 1.08 0.58 1.23 0.82 0.72 1.21 1.87 0.87 2.33 0.66 0.07-0.52 0.28-0.87 0.51-1.07-1.78-0.2-3.64-0.89-3.64-3.95 0-0.87 0.31-1.59 0.82-2.15-0.08-0.2-0.36-1.02 0.08-2.12 0 0 0.67-0.21 2.2 0.82 0.64-0.18 1.32-0.27 2-0.27 0.68 0 1.36 0.09 2 0.27 1.53-1.04 2.2-0.82 2.2-0.82 0.44 1.1 0.16 1.92 0.08 2.12 0.51 0.56 0.82 1.27 0.82 2.15 0 3.07-1.87 3.75-3.65 3.95 0.29 0.25 0.54 0.73 0.54 1.48 0 1.07-0.01 1.93-0.01 2.2 0 0.21 0.15 0.46 0.55 0.38C13.71 14.53 16 11.53 16 8 16 3.58 12.42 0 8 0z"></path></svg>
</a>


      <div class="site-search scoped-search js-site-search" role="search">
          <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/bingjin/ThinkPython2-CN/search" class="js-site-search-form" data-scoped-search-url="/bingjin/ThinkPython2-CN/search" data-unscoped-search-url="/search" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
  <label class="js-chromeless-input-container form-control">
    <div class="scope-badge">This repository</div>
    <input type="text"
      class="form-control js-site-search-focus js-site-search-field is-clearable chromeless-input"
      data-hotkey="s"
      name="q"
      placeholder="Search"
      aria-label="Search this repository"
      data-unscoped-placeholder="Search GitHub"
      data-scoped-placeholder="Search"
      tabindex="1"
      autocapitalize="off">
  </label>
</form>
      </div>

      <ul class="header-nav left" role="navigation">
        <li class="header-nav-item">
          <a href="/pulls" class="js-selected-navigation-item header-nav-link" data-ga-click="Header, click, Nav menu - item:pulls context:user" data-hotkey="g p" data-selected-links="/pulls /pulls/assigned /pulls/mentioned /pulls">
            Pull requests
</a>        </li>
        <li class="header-nav-item">
          <a href="/issues" class="js-selected-navigation-item header-nav-link" data-ga-click="Header, click, Nav menu - item:issues context:user" data-hotkey="g i" data-selected-links="/issues /issues/assigned /issues/mentioned /issues">
            Issues
</a>        </li>
          <li class="header-nav-item">
            <a class="header-nav-link" href="https://gist.github.com/" data-ga-click="Header, go to gist, text:gist">Gist</a>
          </li>
      </ul>

    
<ul class="header-nav user-nav right" id="user-links">
  <li class="header-nav-item">
    
    <a href="/notifications" aria-label="You have unread notifications" class="header-nav-link notification-indicator tooltipped tooltipped-s js-socket-channel js-notification-indicator" data-channel="notification-changed-v2:6568895" data-ga-click="Header, go to notifications, icon:unread" data-hotkey="g n">
        <span class="mail-status unread"></span>
        <svg aria-hidden="true" class="octicon octicon-bell" height="16" role="img" version="1.1" viewBox="0 0 14 16" width="14"><path d="M14 12v1H0v-1l0.73-0.58c0.77-0.77 0.81-2.55 1.19-4.42 0.77-3.77 4.08-5 4.08-5 0-0.55 0.45-1 1-1s1 0.45 1 1c0 0 3.39 1.23 4.16 5 0.38 1.88 0.42 3.66 1.19 4.42l0.66 0.58z m-7 4c1.11 0 2-0.89 2-2H5c0 1.11 0.89 2 2 2z"></path></svg>
</a>
  </li>

  <li class="header-nav-item dropdown js-menu-container">
    <a class="header-nav-link tooltipped tooltipped-s js-menu-target" href="/new"
       aria-label="Create new…"
       data-ga-click="Header, create new, icon:add">
      <svg aria-hidden="true" class="octicon octicon-plus left" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 9H7v5H5V9H0V7h5V2h2v5h5v2z"></path></svg>
      <span class="dropdown-caret"></span>
    </a>

    <div class="dropdown-menu-content js-menu-content">
      <ul class="dropdown-menu dropdown-menu-sw">
        
<a class="dropdown-item" href="/new" data-ga-click="Header, create new repository">
  New repository
</a>


  <a class="dropdown-item" href="/organizations/new" data-ga-click="Header, create new organization">
    New organization
  </a>



  <div class="dropdown-divider"></div>
  <div class="dropdown-header">
    <span title="bingjin/ThinkPython2-CN">This repository</span>
  </div>
    <a class="dropdown-item" href="/bingjin/ThinkPython2-CN/issues/new" data-ga-click="Header, create new issue">
      New issue
    </a>

      </ul>
    </div>
  </li>

  <li class="header-nav-item dropdown js-menu-container">
    <a class="header-nav-link name tooltipped tooltipped-sw js-menu-target" href="/SeikaScarlet"
       aria-label="View profile and more"
       data-ga-click="Header, show menu, icon:avatar">
      <img alt="@SeikaScarlet" class="avatar" height="20" src="https://avatars0.githubusercontent.com/u/6568895?v=3&amp;s=40" width="20" />
      <span class="dropdown-caret"></span>
    </a>

    <div class="dropdown-menu-content js-menu-content">
      <div class="dropdown-menu  dropdown-menu-sw">
        <div class=" dropdown-header header-nav-current-user css-truncate">
            Signed in as <strong class="css-truncate-target">SeikaScarlet</strong>

        </div>


        <div class="dropdown-divider"></div>

          <a class="dropdown-item" href="/SeikaScarlet" data-ga-click="Header, go to profile, text:your profile">
            Your profile
          </a>
        <a class="dropdown-item" href="/stars" data-ga-click="Header, go to starred repos, text:your stars">
          Your stars
        </a>
          <a class="dropdown-item" href="/explore" data-ga-click="Header, go to explore, text:explore">
            Explore
          </a>
          <a class="dropdown-item" href="/integrations" data-ga-click="Header, go to integrations, text:integrations">
            Integrations
          </a>
        <a class="dropdown-item" href="https://help.github.com" data-ga-click="Header, go to help, text:help">
          Help
        </a>


          <div class="dropdown-divider"></div>

          <a class="dropdown-item" href="/settings/profile" data-ga-click="Header, go to settings, icon:settings">
            Settings
          </a>

          <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/logout" class="logout-form" data-form-nonce="781ac8e9c6c1aaed08e5802cfa0e40bddd06cdfb" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="/mEZKWK5vmmipiOXQWi2hUudSnZskPHv12dCqfAUTefbu1I2objtFCq/pB9/M5/U5eKwYLZeEUyGG4qQ7Cvv5g==" /></div>
            <button class="dropdown-item dropdown-signout" data-ga-click="Header, sign out, icon:logout">
              Sign out
            </button>
</form>
      </div>
    </div>
  </li>
</ul>


    
  </div>
</div>

        

      


    <div id="start-of-content" class="accessibility-aid"></div>

      <div id="js-flash-container">
</div>


    <div role="main" class="main-content">
        <div itemscope itemtype="http://schema.org/SoftwareSourceCode">
    <div id="js-repo-pjax-container" data-pjax-container>
      
<div class="pagehead repohead instapaper_ignore readability-menu experiment-repo-nav">
  <div class="container repohead-details-container">

    

<ul class="pagehead-actions">

  <li>
        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/notifications/subscribe" class="js-social-container" data-autosubmit="true" data-form-nonce="781ac8e9c6c1aaed08e5802cfa0e40bddd06cdfb" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="xZjEiCxyCN+FbEsOFRPHk3MU7Sl7kwuFi2Csu+GBze3piGlmk8Vu86waSmZhmlJ47XQomPaV5ef7l2cPnDRl6g==" /></div>      <input class="form-control" id="repository_id" name="repository_id" type="hidden" value="52792140" />

        <div class="select-menu js-menu-container js-select-menu">
          <a href="/bingjin/ThinkPython2-CN/subscription"
            class="btn btn-sm btn-with-count select-menu-button js-menu-target" role="button" tabindex="0" aria-haspopup="true"
            data-ga-click="Repository, click Watch settings, action:blob#show">
            <span class="js-select-button">
              <svg aria-hidden="true" class="octicon octicon-eye" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6c4.94 0 7.94-6 7.94-6S13 2 8.06 2z m-0.06 10c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4z m2-4c0 1.11-0.89 2-2 2s-2-0.89-2-2 0.89-2 2-2 2 0.89 2 2z"></path></svg>
              Watch
            </span>
          </a>
          <a class="social-count js-social-count" href="/bingjin/ThinkPython2-CN/watchers">
            5
          </a>

        <div class="select-menu-modal-holder">
          <div class="select-menu-modal subscription-menu-modal js-menu-content" aria-hidden="true">
            <div class="select-menu-header">
              <svg aria-label="Close" class="octicon octicon-x js-menu-close" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M7.48 8l3.75 3.75-1.48 1.48-3.75-3.75-3.75 3.75-1.48-1.48 3.75-3.75L0.77 4.25l1.48-1.48 3.75 3.75 3.75-3.75 1.48 1.48-3.75 3.75z"></path></svg>
              <span class="select-menu-title">Notifications</span>
            </div>

              <div class="select-menu-list js-navigation-container" role="menu">

                <div class="select-menu-item js-navigation-item selected" role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5L4 13 0 9l1.5-1.5 2.5 2.5 6.5-6.5 1.5 1.5z"></path></svg>
                  <div class="select-menu-item-text">
                    <input checked="checked" id="do_included" name="do" type="radio" value="included" />
                    <span class="select-menu-item-heading">Not watching</span>
                    <span class="description">Be notified when participating or @mentioned.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-eye" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6c4.94 0 7.94-6 7.94-6S13 2 8.06 2z m-0.06 10c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4z m2-4c0 1.11-0.89 2-2 2s-2-0.89-2-2 0.89-2 2-2 2 0.89 2 2z"></path></svg>
                      Watch
                    </span>
                  </div>
                </div>

                <div class="select-menu-item js-navigation-item " role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5L4 13 0 9l1.5-1.5 2.5 2.5 6.5-6.5 1.5 1.5z"></path></svg>
                  <div class="select-menu-item-text">
                    <input id="do_subscribed" name="do" type="radio" value="subscribed" />
                    <span class="select-menu-item-heading">Watching</span>
                    <span class="description">Be notified of all conversations.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-eye" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6c4.94 0 7.94-6 7.94-6S13 2 8.06 2z m-0.06 10c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4z m2-4c0 1.11-0.89 2-2 2s-2-0.89-2-2 0.89-2 2-2 2 0.89 2 2z"></path></svg>
                      Unwatch
                    </span>
                  </div>
                </div>

                <div class="select-menu-item js-navigation-item " role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5L4 13 0 9l1.5-1.5 2.5 2.5 6.5-6.5 1.5 1.5z"></path></svg>
                  <div class="select-menu-item-text">
                    <input id="do_ignore" name="do" type="radio" value="ignore" />
                    <span class="select-menu-item-heading">Ignoring</span>
                    <span class="description">Never be notified.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-mute" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M8 2.81v10.38c0 0.67-0.81 1-1.28 0.53L3 10H1c-0.55 0-1-0.45-1-1V7c0-0.55 0.45-1 1-1h2l3.72-3.72c0.47-0.47 1.28-0.14 1.28 0.53z m7.53 3.22l-1.06-1.06-1.97 1.97-1.97-1.97-1.06 1.06 1.97 1.97-1.97 1.97 1.06 1.06 1.97-1.97 1.97 1.97 1.06-1.06-1.97-1.97 1.97-1.97z"></path></svg>
                      Stop ignoring
                    </span>
                  </div>
                </div>

              </div>

            </div>
          </div>
        </div>
</form>
  </li>

  <li>
    
  <div class="js-toggler-container js-social-container starring-container on">

    <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/bingjin/ThinkPython2-CN/unstar" class="js-toggler-form starred" data-form-nonce="781ac8e9c6c1aaed08e5802cfa0e40bddd06cdfb" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="pqf4qnJibT0uPTMEVPGTHYK494SELiI9nFcuz1UX5jP7UCZXF7JjoIfeuwCweO9B9YHO5NovXbtWVwGa49qeqw==" /></div>
      <button
        class="btn btn-sm btn-with-count js-toggler-target"
        aria-label="Unstar this repository" title="Unstar bingjin/ThinkPython2-CN"
        data-ga-click="Repository, click unstar button, action:blob#show; text:Unstar">
        <svg aria-hidden="true" class="octicon octicon-star" height="16" role="img" version="1.1" viewBox="0 0 14 16" width="14"><path d="M14 6l-4.9-0.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14l4.33-2.33 4.33 2.33L10.4 9.26 14 6z"></path></svg>
        Unstar
      </button>
        <a class="social-count js-social-count" href="/bingjin/ThinkPython2-CN/stargazers">
          27
        </a>
</form>
    <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/bingjin/ThinkPython2-CN/star" class="js-toggler-form unstarred" data-form-nonce="781ac8e9c6c1aaed08e5802cfa0e40bddd06cdfb" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="fVZpzF30tVCC1aYCVA8N8H+b80W5lisRgGB46xUcUkqbrkW2W+pvIVwulXExQtYz+d5xWAbj+9BeXLjBIBfE3A==" /></div>
      <button
        class="btn btn-sm btn-with-count js-toggler-target"
        aria-label="Star this repository" title="Star bingjin/ThinkPython2-CN"
        data-ga-click="Repository, click star button, action:blob#show; text:Star">
        <svg aria-hidden="true" class="octicon octicon-star" height="16" role="img" version="1.1" viewBox="0 0 14 16" width="14"><path d="M14 6l-4.9-0.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14l4.33-2.33 4.33 2.33L10.4 9.26 14 6z"></path></svg>
        Star
      </button>
        <a class="social-count js-social-count" href="/bingjin/ThinkPython2-CN/stargazers">
          27
        </a>
</form>  </div>

  </li>

  <li>
          <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/bingjin/ThinkPython2-CN/fork" class="btn-with-count" data-form-nonce="781ac8e9c6c1aaed08e5802cfa0e40bddd06cdfb" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="hvPn9BwK31upcm2d2nOstSFDiYNaXapEtCGdiNLUcFrcC96nkW5eqz2MWn6OWCcxNy79t4i/cIqMBEMJFZ4zOg==" /></div>
            <button
                type="submit"
                class="btn btn-sm btn-with-count"
                data-ga-click="Repository, show fork modal, action:blob#show; text:Fork"
                title="Fork your own copy of bingjin/ThinkPython2-CN to your account"
                aria-label="Fork your own copy of bingjin/ThinkPython2-CN to your account">
              <svg aria-hidden="true" class="octicon octicon-repo-forked" height="16" role="img" version="1.1" viewBox="0 0 10 16" width="10"><path d="M8 1c-1.11 0-2 0.89-2 2 0 0.73 0.41 1.38 1 1.72v1.28L5 8 3 6v-1.28c0.59-0.34 1-0.98 1-1.72 0-1.11-0.89-2-2-2S0 1.89 0 3c0 0.73 0.41 1.38 1 1.72v1.78l3 3v1.78c-0.59 0.34-1 0.98-1 1.72 0 1.11 0.89 2 2 2s2-0.89 2-2c0-0.73-0.41-1.38-1-1.72V9.5l3-3V4.72c0.59-0.34 1-0.98 1-1.72 0-1.11-0.89-2-2-2zM2 4.2c-0.66 0-1.2-0.55-1.2-1.2s0.55-1.2 1.2-1.2 1.2 0.55 1.2 1.2-0.55 1.2-1.2 1.2z m3 10c-0.66 0-1.2-0.55-1.2-1.2s0.55-1.2 1.2-1.2 1.2 0.55 1.2 1.2-0.55 1.2-1.2 1.2z m3-10c-0.66 0-1.2-0.55-1.2-1.2s0.55-1.2 1.2-1.2 1.2 0.55 1.2 1.2-0.55 1.2-1.2 1.2z"></path></svg>
              Fork
            </button>
</form>
    <a href="/bingjin/ThinkPython2-CN/network" class="social-count">
      18
    </a>
  </li>
</ul>

    <h1 class="entry-title public ">
  <svg aria-hidden="true" class="octicon octicon-repo" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M4 9h-1v-1h1v1z m0-3h-1v1h1v-1z m0-2h-1v1h1v-1z m0-2h-1v1h1v-1z m8-1v12c0 0.55-0.45 1-1 1H6v2l-1.5-1.5-1.5 1.5V14H1c-0.55 0-1-0.45-1-1V1C0 0.45 0.45 0 1 0h10c0.55 0 1 0.45 1 1z m-1 10H1v2h2v-1h3v1h5V11z m0-10H2v9h9V1z"></path></svg>
  <span class="author" itemprop="author"><a href="/bingjin" class="url fn" rel="author">bingjin</a></span><!--
--><span class="path-divider">/</span><!--
--><strong itemprop="name"><a href="/bingjin/ThinkPython2-CN" data-pjax="#js-repo-pjax-container">ThinkPython2-CN</a></strong>

</h1>

  </div>
  <div class="container">
    
<nav class="reponav js-repo-nav js-sidenav-container-pjax"
     itemscope
     itemtype="http://schema.org/BreadcrumbList"
     role="navigation"
     data-pjax="#js-repo-pjax-container">

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a href="/bingjin/ThinkPython2-CN" aria-selected="true" class="js-selected-navigation-item selected reponav-item" data-hotkey="g c" data-selected-links="repo_source repo_downloads repo_commits repo_releases repo_tags repo_branches /bingjin/ThinkPython2-CN" itemprop="url">
      <svg aria-hidden="true" class="octicon octicon-code" height="16" role="img" version="1.1" viewBox="0 0 14 16" width="14"><path d="M9.5 3l-1.5 1.5 3.5 3.5L8 11.5l1.5 1.5 4.5-5L9.5 3zM4.5 3L0 8l4.5 5 1.5-1.5L2.5 8l3.5-3.5L4.5 3z"></path></svg>
      <span itemprop="name">Code</span>
      <meta itemprop="position" content="1">
</a>  </span>

    <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
      <a href="/bingjin/ThinkPython2-CN/issues" class="js-selected-navigation-item reponav-item" data-hotkey="g i" data-selected-links="repo_issues repo_labels repo_milestones /bingjin/ThinkPython2-CN/issues" itemprop="url">
        <svg aria-hidden="true" class="octicon octicon-issue-opened" height="16" role="img" version="1.1" viewBox="0 0 14 16" width="14"><path d="M7 2.3c3.14 0 5.7 2.56 5.7 5.7S10.14 13.7 7 13.7 1.3 11.14 1.3 8s2.56-5.7 5.7-5.7m0-1.3C3.14 1 0 4.14 0 8s3.14 7 7 7 7-3.14 7-7S10.86 1 7 1z m1 3H6v5h2V4z m0 6H6v2h2V10z"></path></svg>
        <span itemprop="name">Issues</span>
        <span class="counter">0</span>
        <meta itemprop="position" content="2">
</a>    </span>

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a href="/bingjin/ThinkPython2-CN/pulls" class="js-selected-navigation-item reponav-item" data-hotkey="g p" data-selected-links="repo_pulls /bingjin/ThinkPython2-CN/pulls" itemprop="url">
      <svg aria-hidden="true" class="octicon octicon-git-pull-request" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M11 11.28c0-1.73 0-6.28 0-6.28-0.03-0.78-0.34-1.47-0.94-2.06s-1.28-0.91-2.06-0.94c0 0-1.02 0-1 0V0L4 3l3 3V4h1c0.27 0.02 0.48 0.11 0.69 0.31s0.3 0.42 0.31 0.69v6.28c-0.59 0.34-1 0.98-1 1.72 0 1.11 0.89 2 2 2s2-0.89 2-2c0-0.73-0.41-1.38-1-1.72z m-1 2.92c-0.66 0-1.2-0.55-1.2-1.2s0.55-1.2 1.2-1.2 1.2 0.55 1.2 1.2-0.55 1.2-1.2 1.2zM4 3c0-1.11-0.89-2-2-2S0 1.89 0 3c0 0.73 0.41 1.38 1 1.72 0 1.55 0 5.56 0 6.56-0.59 0.34-1 0.98-1 1.72 0 1.11 0.89 2 2 2s2-0.89 2-2c0-0.73-0.41-1.38-1-1.72V4.72c0.59-0.34 1-0.98 1-1.72z m-0.8 10c0 0.66-0.55 1.2-1.2 1.2s-1.2-0.55-1.2-1.2 0.55-1.2 1.2-1.2 1.2 0.55 1.2 1.2z m-1.2-8.8c-0.66 0-1.2-0.55-1.2-1.2s0.55-1.2 1.2-1.2 1.2 0.55 1.2 1.2-0.55 1.2-1.2 1.2z"></path></svg>
      <span itemprop="name">Pull requests</span>
      <span class="counter">0</span>
      <meta itemprop="position" content="3">
</a>  </span>

    <a href="/bingjin/ThinkPython2-CN/wiki" class="js-selected-navigation-item reponav-item" data-hotkey="g w" data-selected-links="repo_wiki /bingjin/ThinkPython2-CN/wiki">
      <svg aria-hidden="true" class="octicon octicon-book" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M2 5h4v1H2v-1z m0 3h4v-1H2v1z m0 2h4v-1H2v1z m11-5H9v1h4v-1z m0 2H9v1h4v-1z m0 2H9v1h4v-1z m2-6v9c0 0.55-0.45 1-1 1H8.5l-1 1-1-1H1c-0.55 0-1-0.45-1-1V3c0-0.55 0.45-1 1-1h5.5l1 1 1-1h5.5c0.55 0 1 0.45 1 1z m-8 0.5l-0.5-0.5H1v9h6V3.5z m7-0.5H8.5l-0.5 0.5v8.5h6V3z"></path></svg>
      Wiki
</a>
  <a href="/bingjin/ThinkPython2-CN/pulse" class="js-selected-navigation-item reponav-item" data-selected-links="pulse /bingjin/ThinkPython2-CN/pulse">
    <svg aria-hidden="true" class="octicon octicon-pulse" height="16" role="img" version="1.1" viewBox="0 0 14 16" width="14"><path d="M11.5 8L8.8 5.4 6.6 8.5 5.5 1.6 2.38 8H0V10h3.6L4.5 8.2l0.9 5.4L9 8.5l1.6 1.5H14V8H11.5z"></path></svg>
    Pulse
</a>
  <a href="/bingjin/ThinkPython2-CN/graphs" class="js-selected-navigation-item reponav-item" data-selected-links="repo_graphs repo_contributors /bingjin/ThinkPython2-CN/graphs">
    <svg aria-hidden="true" class="octicon octicon-graph" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M16 14v1H0V0h1v14h15z m-11-1H3V8h2v5z m4 0H7V3h2v10z m4 0H11V6h2v7z"></path></svg>
    Graphs
</a>

</nav>

  </div>
</div>

<div class="container new-discussion-timeline experiment-repo-nav">
  <div class="repository-content">

    

<a href="/bingjin/ThinkPython2-CN/blob/be45b1b96510a894aa01b7254b624afaf5bbb7f6/source/04-case-study-interface-design.rst" class="hidden js-permalink-shortcut" data-hotkey="y">Permalink</a>

<!-- blob contrib key: blob_contributors:v21:14c46d36c93f7a6d6701b94096a69cb3 -->

<div class="file-navigation js-zeroclipboard-container">
  
<div class="select-menu js-menu-container js-select-menu left">
  <button class="btn btn-sm select-menu-button js-menu-target css-truncate" data-hotkey="w"
    title="master"
    type="button" aria-label="Switch branches or tags" tabindex="0" aria-haspopup="true">
    <i>Branch:</i>
    <span class="js-select-button css-truncate-target">master</span>
  </button>

  <div class="select-menu-modal-holder js-menu-content js-navigation-container" data-pjax aria-hidden="true">

    <div class="select-menu-modal">
      <div class="select-menu-header">
        <svg aria-label="Close" class="octicon octicon-x js-menu-close" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M7.48 8l3.75 3.75-1.48 1.48-3.75-3.75-3.75 3.75-1.48-1.48 3.75-3.75L0.77 4.25l1.48-1.48 3.75 3.75 3.75-3.75 1.48 1.48-3.75 3.75z"></path></svg>
        <span class="select-menu-title">Switch branches/tags</span>
      </div>

      <div class="select-menu-filters">
        <div class="select-menu-text-filter">
          <input type="text" aria-label="Filter branches/tags" id="context-commitish-filter-field" class="form-control js-filterable-field js-navigation-enable" placeholder="Filter branches/tags">
        </div>
        <div class="select-menu-tabs">
          <ul>
            <li class="select-menu-tab">
              <a href="#" data-tab-filter="branches" data-filter-placeholder="Filter branches/tags" class="js-select-menu-tab" role="tab">Branches</a>
            </li>
            <li class="select-menu-tab">
              <a href="#" data-tab-filter="tags" data-filter-placeholder="Find a tag…" class="js-select-menu-tab" role="tab">Tags</a>
            </li>
          </ul>
        </div>
      </div>

      <div class="select-menu-list select-menu-tab-bucket js-select-menu-tab-bucket" data-tab-filter="branches" role="menu">

        <div data-filterable-for="context-commitish-filter-field" data-filterable-type="substring">


            <a class="select-menu-item js-navigation-item js-navigation-open selected"
               href="/bingjin/ThinkPython2-CN/blob/master/source/04-case-study-interface-design.rst"
               data-name="master"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5L4 13 0 9l1.5-1.5 2.5 2.5 6.5-6.5 1.5 1.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="master">
                master
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/bingjin/ThinkPython2-CN/blob/tex/source/04-case-study-interface-design.rst"
               data-name="tex"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5L4 13 0 9l1.5-1.5 2.5 2.5 6.5-6.5 1.5 1.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="tex">
                tex
              </span>
            </a>
        </div>

          <div class="select-menu-no-results">Nothing to show</div>
      </div>

      <div class="select-menu-list select-menu-tab-bucket js-select-menu-tab-bucket" data-tab-filter="tags">
        <div data-filterable-for="context-commitish-filter-field" data-filterable-type="substring">


        </div>

        <div class="select-menu-no-results">Nothing to show</div>
      </div>

    </div>
  </div>
</div>

  <div class="btn-group right">
    <a href="/bingjin/ThinkPython2-CN/find/master"
          class="js-pjax-capture-input btn btn-sm"
          data-pjax
          data-hotkey="t">
      Find file
    </a>
    <button aria-label="Copy file path to clipboard" class="js-zeroclipboard btn btn-sm zeroclipboard-button tooltipped tooltipped-s" data-copied-hint="Copied!" type="button">Copy path</button>
  </div>
  <div class="breadcrumb js-zeroclipboard-target">
    <span class="repo-root js-repo-root"><span class="js-path-segment"><a href="/bingjin/ThinkPython2-CN"><span>ThinkPython2-CN</span></a></span></span><span class="separator">/</span><span class="js-path-segment"><a href="/bingjin/ThinkPython2-CN/tree/master/source"><span>source</span></a></span><span class="separator">/</span><strong class="final-path">04-case-study-interface-design.rst</strong>
  </div>
</div>


  <div class="commit-tease">
      <span class="right">
        <a class="commit-tease-sha" href="/bingjin/ThinkPython2-CN/commit/be45b1b96510a894aa01b7254b624afaf5bbb7f6" data-pjax>
          be45b1b
        </a>
        <time datetime="2016-03-22T15:16:40Z" is="relative-time">Mar 22, 2016</time>
      </span>
      <div>
        <img alt="@bingjin" class="avatar" height="20" src="https://avatars3.githubusercontent.com/u/14083704?v=3&amp;s=40" width="20" />
        <a href="/bingjin" class="user-mention" rel="author">bingjin</a>
          <a href="/bingjin/ThinkPython2-CN/commit/be45b1b96510a894aa01b7254b624afaf5bbb7f6" class="message" data-pjax="true" title="update 7">update 7</a>
      </div>

    <div class="commit-tease-contributors">
      <button type="button" class="btn-link muted-link contributors-toggle" data-facebox="#blob_contributors_box">
        <strong>1</strong>
         contributor
      </button>
      
    </div>

    <div id="blob_contributors_box" style="display:none">
      <h2 class="facebox-header" data-facebox-id="facebox-header">Users who have contributed to this file</h2>
      <ul class="facebox-user-list" data-facebox-id="facebox-description">
          <li class="facebox-user-list-item">
            <img alt="@bingjin" height="24" src="https://avatars1.githubusercontent.com/u/14083704?v=3&amp;s=48" width="24" />
            <a href="/bingjin">bingjin</a>
          </li>
      </ul>
    </div>
  </div>

<div class="file">
  <div class="file-header">
  <div class="file-actions">

    <div class="btn-group">
      <a href="/bingjin/ThinkPython2-CN/raw/master/source/04-case-study-interface-design.rst" class="btn btn-sm " id="raw-url">Raw</a>
        <a href="/bingjin/ThinkPython2-CN/blame/master/source/04-case-study-interface-design.rst" class="btn btn-sm js-update-url-with-hash">Blame</a>
      <a href="/bingjin/ThinkPython2-CN/commits/master/source/04-case-study-interface-design.rst" class="btn btn-sm " rel="nofollow">History</a>
    </div>

        <a class="btn-octicon tooltipped tooltipped-nw"
           href="github-windows://openRepo/https://github.com/bingjin/ThinkPython2-CN?branch=master&amp;filepath=source%2F04-case-study-interface-design.rst"
           aria-label="Open this file in GitHub Desktop"
           data-ga-click="Repository, open with desktop, type:windows">
            <svg aria-hidden="true" class="octicon octicon-device-desktop" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M15 2H1c-0.55 0-1 0.45-1 1v9c0 0.55 0.45 1 1 1h5.34c-0.25 0.61-0.86 1.39-2.34 2h8c-1.48-0.61-2.09-1.39-2.34-2h5.34c0.55 0 1-0.45 1-1V3c0-0.55-0.45-1-1-1z m0 9H1V3h14v8z"></path></svg>
        </a>

        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/bingjin/ThinkPython2-CN/edit/master/source/04-case-study-interface-design.rst" class="inline-form js-update-url-with-hash" data-form-nonce="781ac8e9c6c1aaed08e5802cfa0e40bddd06cdfb" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="SXlwU6+QoJasolpwZXeYO2aZD3eiZDKqXM/fMgOBuWOK4TwHeWC/lhdVJ8xvUfXqA5Fjg1/8n8ftkwXJrcvPLg==" /></div>
          <button class="btn-octicon tooltipped tooltipped-nw" type="submit"
            aria-label="Edit the file in your fork of this project" data-hotkey="e" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-pencil" height="16" role="img" version="1.1" viewBox="0 0 14 16" width="14"><path d="M0 12v3h3l8-8-3-3L0 12z m3 2H1V12h1v1h1v1z m10.3-9.3l-1.3 1.3-3-3 1.3-1.3c0.39-0.39 1.02-0.39 1.41 0l1.59 1.59c0.39 0.39 0.39 1.02 0 1.41z"></path></svg>
          </button>
</form>        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/bingjin/ThinkPython2-CN/delete/master/source/04-case-study-interface-design.rst" class="inline-form" data-form-nonce="781ac8e9c6c1aaed08e5802cfa0e40bddd06cdfb" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="nboUBB9Dj7Afm6ebJTMTj78se8kkvl/mvPbAvIR2TvzDHIDqTIWT4GIppfP/IFYk9vO22D/2XqFnG9h+j8bGXg==" /></div>
          <button class="btn-octicon btn-octicon-danger tooltipped tooltipped-nw" type="submit"
            aria-label="Delete the file in your fork of this project" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-trashcan" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M10 2H8c0-0.55-0.45-1-1-1H4c-0.55 0-1 0.45-1 1H1c-0.55 0-1 0.45-1 1v1c0 0.55 0.45 1 1 1v9c0 0.55 0.45 1 1 1h7c0.55 0 1-0.45 1-1V5c0.55 0 1-0.45 1-1v-1c0-0.55-0.45-1-1-1z m-1 12H2V5h1v8h1V5h1v8h1V5h1v8h1V5h1v9z m1-10H1v-1h9v1z"></path></svg>
          </button>
</form>  </div>

  <div class="file-info">
      527 lines (348 sloc)
      <span class="file-info-divider"></span>
    19.8 KB
  </div>
</div>

  
  <div id="readme" class="readme blob instapaper_body">
    <article class="markdown-body entry-content" itemprop="text"><h1><a id="user-content-第四章案例研究接口设计" class="anchor" href="#第四章案例研究接口设计" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>第四章：案例研究：接口设计</h1>
<p>本章将通过一个案例研究，介绍如何设计出相互配合的函数。</p>
<p>本章会介绍 <code>turtle</code> 模块，它可以让你使用海龟图形（turtle graphics）绘制图像。大部分的Python安装环境下都包含了这个模块，但是如果你是在PythonAnywhere上运行Python的，你将无法运行本章中的代码示例（至少在我写这章时是做不到的）。</p>
<p>如果你已经在自己的电脑上安装了Python，那么不会有问题。如果没有，现在就是安装Python的好时机。我在 <a href="http://tinyurl.com/thinkpython2e">http://tinyurl.com/thinkpython2e</a> 这个页面上发布了相关指南。</p>
<p>本章的示例代码可以从<a href="http://thinkpython2.com/code/polygon.py">http://thinkpython2.com/code/polygon.py</a> 获得。</p>
<a name="user-content-turtle"></a>
<h2><a id="user-content-turtle模块" class="anchor" href="#turtle模块" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>turtle模块</h2>
<p>打开Python解释器，输入以下代码，检查你是否安装了 <code>turltle</code> 模块：</p>
<pre>&gt;&gt;&gt; import turtle
&gt;&gt;&gt; bob = turtle.Turtle()
</pre>
<p>上述代码运行后，应该会新建一个窗口，窗口中间有一个小箭头，代表的就是海龟。现在关闭窗口。</p>
<p>新建一个名叫  <code>mypolygon.py</code> 的文件，输入以下代码：</p>
<pre>import turtle
bob = turtle.Turtle()
print(bob)
turtle.mainloop()
</pre>
<p><code>turtle</code> 模块（小写的t）提供了一个叫作 <code>Turtle</code> 的函数（大写的T），这个函数会创建一个 <code>Turtle</code> 对象，我们将其赋值给名为 <code>bob</code> 的变量。打印 <code>bob</code> 的话，会输出下面这样的结果：</p>
<pre>&lt;turtle.Turtle object at 0xb7bfbf4c&gt;
</pre>
<p>这意味着，<code>bob</code> 指向一个类型为Turtle的对象，这个类型是由 <code>turtle</code> 模块定义的。</p>
<p><code>mainloop</code> 告诉窗口等待用户操作，尽管在这个例子中，用户除了关闭窗口之外，并没有其他可做的事情。</p>
<p>创建了一个 <code>Turtle</code> 对象之后，你可以调用 <strong>方法（method）</strong> 来在窗口中移动该对象。方法与函数类似，但是其语法略有不同。例如，要让海龟向前走：</p>
<pre>bob.fd(100)
</pre>
<p>方法 <code>fd</code> 与我们称之为 <code>bob</code> 的对象是相关联的。调用方法就像提出一个请求：你在请求 <code>bob</code> 往前走。</p>
<p><code>fd</code> 方法的实参是像素距离，所以实际前进的距离取决于你的屏幕。</p>
<p><code>Turtle</code> 对象中你能调用的其他方法还包括：让它向后走的 <code>bk</code> ，向左转的 <code>lt</code> ，向右转的 <code>rt</code> 。 <code>lt</code> 和 <code>rt</code> 这两个方法接受的实参是角度。</p>
<p>另外，每个 <code>Turtle</code> 都握着一支笔，不是落笔就是抬笔；如果落笔了，<code>Turtle</code> 就会在移动时留下痕迹。<code>pu</code> 和 <code>pd</code> 这两个方法分别代表“抬笔（pen up）”和“落笔（pen down）”。</p>
<p>如果要画一个直角（right angle），请在程序中添加以下代码（放在创建 <code>bob</code> 之后，调用 <code>mainloop</code> 之前）：</p>
<pre>bob.fd(100)
bob.lt(90)
bob.fd(100)
</pre>
<p>当你运行此程序时，你应该会看到 <code>bob</code> 先朝东移动，然后向北移动，同时在身后留下两条线段（line segment）。</p>
<p>现在修改程序，画一个正方形。在没有成功之前，不要继续往下看。</p>
<a name="user-content-id2"></a>
<h2><a id="user-content-简单的重复" class="anchor" href="#简单的重复" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>简单的重复</h2>
<p>很有可能你刚才写了像下面这样的一个程序：</p>
<pre>bob.fd(100)
bob.lt(90)

bob.fd(100)
bob.lt(90)

bob.fd(100)
bob.lt(90)

bob.fd(100)
</pre>
<p>我们可以利用一个 <code>for</code> 语句，以更简洁的代码来做相同的事情。
将下面的示例代码加入 <code>mypolygon.py</code> ，并重新运行：</p>
<pre>for i in range(4):
    print('Hello!')
</pre>
<p>你应该会看到如下输出：</p>
<pre>Hello!
Hello!
Hello!
Hello!
</pre>
<p>这是 <code>for</code> 语句最简单的用法；后面我们会介绍更多的用法。
但是这对于让你重写画正方形的程序已经足够了。 如果没有完成，请不要往下看。</p>
<p>下面是一个画正方形的 <code>for</code> 语句：</p>
<pre>for i in range(4):
    bob.fd(100)
    bob.lt(90)
</pre>
<p>for语句的语法和函数定义类似。
它有一个以冒号结尾的语句头（header）以及一个缩进的语句体（body）。
语句体可以包含任意条语句。</p>
<p><code>for</code> 语句有时也被称为<strong>循环（loop）</strong>，因为执行流程会贯穿整个语句体，然后再循环回顶部。
在此例中，它将运行语句体四次。</p>
<p>这个版本事实上和前面画正方形的代码有所不同，因为它在画完正方形的最后一条边后，
又多转了一下。这个额外的转动多花了些时间，
但是如果我们每次都通过循环来做这件事情，这样反而是简化了代码。
这个版本还让海龟回到了初始位置，朝向也与出发时一致。</p>
<a name="user-content-id3"></a>
<h2><a id="user-content-练习" class="anchor" href="#练习" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>练习</h2>
<p>下面是一系列学习使用 <code>Turtle</code> 的练习。
这些练习虽说是为了好玩，但是也有自己的目的。
你在做这些练习的时候，想一想它们的目的是什么。</p>
<blockquote>
译者注：原文中使用的还是 <code>TurtleWorld</code> ，应该是作者忘了修改。</blockquote>
<p>后面几节是中介绍了这些练习的答案，因此如果你还没完成（或者至少试过），请不要看答案。</p>
<ol>
<li><p>写一个名为 <code>square</code> 的函数，接受一个名为 <code>t</code> 的形参，<code>t</code> 是一个海龟。
这个函数应用这只海龟画一个正方形。</p>
<p>写一个函数调用，将 <code>bob</code> 作为实参传给 <code>square</code> ，然后再重新运行程序。</p>
</li>
<li><p>给 <code>square</code> 增加另一个名为 <code>length</code> 的形参。
修改函数体，使得正方形边的长度是 <code>length</code> ，然后修改函数调用，提供第二个实参。
重新运行程序。用一系列 <code>length</code> 值测试你的程序。</p>
</li>
<li><p>复制 <code>square</code> ，并将函数改名为 <code>polygon</code> 。
增加另外一个名为 <code>n</code> 的形参并修改函数体，让它画一个正n边形（n-sided regular polygon）。
提示：正n边形的外角是<tt>
360/n</tt>
度。</p>
</li>
<li><p>编写一个名为 <code>circle</code> 的函数，它接受一个海龟t和半径r作为形参，
然后以合适的边长和边数调用 <code>polygon</code> ，画一个近似圆形。
用一系列r值测试你的函数。</p>
<p>提示：算出圆的周长，并确保 <code>length * n = circumference</code> 。</p>
</li>
<li><p>完成一个更泛化（general）的 <code>circle</code> 函数，称其为 <code>arc</code> ，接受一个额外的参数 <code>angle</code> ，确定画多完整的圆。<code>angle</code> 的单位是度，因此当 <code>angle=360</code> 时， <code>arc</code>
应该画一个完整的圆。</p>
</li>
</ol>
<a name="user-content-id4"></a>
<h2><a id="user-content-封装" class="anchor" href="#封装" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>封装</h2>
<p>第一个练习要求你将画正方形的代码放到一个函数定义中,然后调用该函数，
将海龟作为形参传递给它。下面是一个解法：</p>
<pre>def square(t):
    for i in range(4):
        t.fd(100)
        t.lt(90)

square(bob)
</pre>
<p>最内层的语句 <code>fd</code> 和 <code>lt</code> 被缩进两次，以显示它们处在 <code>for</code> 循环内，
而该循环又在函数定义内。下一行 <code>square(bob)</code> 和左边界（left margin）对齐，
表示 <code>for</code> 循环和函数定义结束。</p>
<p>在函数内部，<code>t</code> 指的是同一只海龟 <code>bob</code> ， 所以 <code>t.lt(90)</code> 和 <code>bob.lt(90)</code> 的效果相同。
那么既然这样，为什么不将形参命名为 <code>bob</code> 呢？ 因为 <code>t</code> 可以是任何海龟而不仅仅是 <code>bob</code> ，
也就是说你可以创建第二只海龟，并且将它作为实参传递给 <code>square</code> ：</p>
<pre>alice = Turtle()
square(alice)
</pre>
<p>将一部分代码包装在函数里被称作 <strong>encapsulation（封装）</strong>。
封装的好处之一，为这些代码赋予一个名字，
这充当了某种文档说明。另一个好处是，如果你重复使用这些代码，
调用函数两次比拷贝粘贴函数体要更加简洁！</p>
<a name="user-content-id5"></a>
<h2><a id="user-content-泛化" class="anchor" href="#泛化" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>泛化</h2>
<p>下一个练习是给 <code>square</code> 增加一个 <code>length</code> 形参。下面是一个解法：</p>
<pre>def square(t, length):
    for i in range(4):
        t.fd(length)
        t.lt(90)

square(bob, 100)
</pre>
<p>为函数增加一个形参被称作<strong>泛化（generalization）</strong>，
因为这使得函数更通用：在前面的版本中，
正方形的边长总是一样的；此版本中，它可以是任意大小。</p>
<p>下一个练习也是泛化。泛化之后不再是只能画一个正方形，<code>polygon</code> 可以画任意的正多边形。
下面是一个解法：</p>
<pre>def polygon(t, n, length):
    angle = 360 / n
    for i in range(n):
        t.fd(length)
        t.lt(angle)

polygon(bob, 7, 70)
</pre>
<p>这个示例代码画了一个边长为70的七边形。</p>
<p>如果你在使用Python 2，<code>angle</code> 的值可能由于整型数除法（integer division）出现偏差。一个简单的解决办法是这样计算 <code>angle</code> ：<code>angle = 360.0 / n</code>。因为分子（numerator）是一个浮点数，最终的结果也会是一个浮点数。</p>
<p>如果一个函数有几个数字实参，很容易忘记它们是什么或者它们的顺序。在这种情况下，
在实参列表中加入形参的名称是通常是一个很好的办法：</p>
<pre>polygon(bob, n=7, length=70)
</pre>
<p>这些被称作<strong>关键字实参（keyword arguments）</strong>，
因为它们j加上了形参名作为“关键字”（不要和Python的关键字搞混了，如 <code>while</code> 和 <code>def</code> ）。</p>
<p>这一语法使得程序的可读性更强。它也提醒了我们实参和形参的工作方式：
当你调用函数时，实参被赋给形参。</p>
<a name="user-content-id6"></a>
<h2><a id="user-content-接口设计" class="anchor" href="#接口设计" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>接口设计</h2>
<p>下一个练习是编写接受半径r作为形参的 <code>circle</code> 函数。
下面是一个使用 <code>polygon</code> 画一个50边形的简单解法：</p>
<pre>import math

def circle(t, r):
    circumference = 2 * math.pi * r
    n = 50
    length = circumference / n
    polygon(t, n, length)
</pre>
<p>函数的第一行通过半径r计算圆的周长，公式是<tt>
2 \pi r</tt>
。
由于用了 <code>math.pi</code> ，我们需要导入 <code>math</code> 模块。
按照惯例，<code>import</code> 语句通常位于脚本的开始位置。</p>
<p>n是我们的近似圆中线段的条数， <code>length</code> 是每一条线段的长度。
这样 <code>polygon</code> 画出的就是一个50边形，近似一个半径为r的圆。</p>
<p>这种解法的一个局限在于，n是一个常量，意味着对于非常大的圆，
线段会非常长，而对于小圆，我们会浪费时间画非常小的线段。
一个解决方案是将n作为形参，泛化函数。
这将给用户（调用 <code>circle</code> 的人）更多的掌控力， 但是接口就不那么干净了。</p>
<p>函数的<strong>接口（interface）</strong>是一份关于如何使用该函数的总结：
形参是什么？函数做什么？返回值是什么？
如果接口让调用者避免处理不必要的细节，直接做自己想做的式，那么这个接口就是“干净的”。</p>
<p>在这个例子中，<code>r</code> 属于接口的一部分，因为它指定了要画多大的圆。
n就不太合适，因为它是关于 <strong>如何</strong> 画圆的细节。</p>
<p>与其把接口弄乱，不如根据周长（circumference）选择一个合适的n值：</p>
<pre>def circle(t, r):
    circumference = 2 * math.pi * r
    n = int(circumference / 3) + 1
    length = circumference / n
    polygon(t, n, length)
</pre>
<p>现在线段的数量，是约为周长三分之一的整型数，
所以每条线段的长度（大概）是3，小到足以使圆看上去逼真，
又大到效率足够高，对任意大小的圆都能接受。</p>
<a name="user-content-id7"></a>
<h2><a id="user-content-重构" class="anchor" href="#重构" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>重构</h2>
<p>当我写 <code>circle</code> 程序的时候，我能够复用 <code>polygon</code> ，
因为一个多边形是与圆形非常近似。
但是 <code>arc</code> 就不那么容易实现了；我们不能使用 <code>polygon</code> 或者 <code>circle</code> 来画一个弧。</p>
<p>一种替代方案是从复制 <code>polygon</code> 开始，
然后将它转化为 <code>arc</code> 。最后的函数看上去可像这样：</p>
<pre>def arc(t, r, angle):
    arc_length = 2 * math.pi * r * angle / 360
    n = int(arc_length / 3) + 1
    step_length = arc_length / n
    step_angle = angle / n

    for i in range(n):
        t.fd(step_length)
        t.lt(step_angle)
</pre>
<p>该函数的后半部分看上去很像 <code>polygon</code> ，
但是在不改变接口的条件下，我们无法复用 <code>polygon</code> 。
我们可以泛化 <code>polygon</code> 来接受一个角度作为第三个实参，
但是这样 <code>polygon</code> 就不再是一个合适的名字了！
让我们称这个更通用的函数为 <code>polyline</code> ：</p>
<pre>def polyline(t, n, length, angle):
    for i in range(n):
        t.fd(length)
        t.lt(angle)
</pre>
<p>现在，我们可以用 <code>polyline</code> 重写 <code>polygon</code> 和 <code>arc</code> ：</p>
<pre>def polygon(t, n, length):
    angle = 360.0 / n
    polyline(t, n, length, angle)

def arc(t, r, angle):
    arc_length = 2 * math.pi * r * angle / 360
    n = int(arc_length / 3) + 1
    step_length = arc_length / n
    step_angle = float(angle) / n
    polyline(t, n, step_length, step_angle)
</pre>
<p>最后，我们可以用 <code>arc</code> 重写 <code>circle</code> ：</p>
<pre>def circle(t, r):
    arc(t, r, 360)
</pre>
<p>重新整理一个程序以改进函数接口和促进代码复用的这个过程，
被称作<strong>重构（refactoring）</strong>。
在此例中，我们注意到 <code>arc</code> 和 <code>polygon</code> 中有相似的代码，
因此，我们“将它分解出来”（factor it out），放入 <code>polyline</code> 函数。</p>
<p>如果我们提前已经计划好了，我们可能会首先写 <code>polyline</code> 函数，避免重构，
但是在一个项目开始的时候，你常常并不知道那么多，不能设计好全部的接口。
一旦你开始编码后，你才能更好地理解问题。
有时重构是一个说明你已经学到某些东西的预兆。</p>
<a name="user-content-id8"></a>
<h2><a id="user-content-开发方案" class="anchor" href="#开发方案" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>开发方案</h2>
<p><strong>开发计划（development plan）</strong>是一种编写程序的过程。
此例中我们使用的过程是“封装和泛化”。 这个过程的具体步骤是：</p>
<ol>
<li>从写一个没有函数定义的小程序开始。</li>
<li>一旦该程序运行正常，找出其中相关性强的部分，将它们封装进一个函数并给它一个名字。</li>
<li>通过增加适当的形参，泛化该函数。</li>
<li>重复1–3步，直到你有一些可正常运行的函数。
复制粘贴有用的代码，避免重复输入（和重新调试）。</li>
<li>寻找机会通过重构改进程序。
例如，如果在多个地方有相似的代码，考虑将它分解到一个合适的通用函数中。</li>
</ol>
<p>这个过程也有一些缺点。后面我们将介绍其他替代方案，
但是如果你事先不知道如何将程序分解为函数，这是个很有用办法。
该方法可以让你一边编程，一边设计。</p>
<a name="user-content-id9"></a>
<h2><a id="user-content-文档字符串" class="anchor" href="#文档字符串" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>文档字符串</h2>
<p><strong>文档字符串（docstring）</strong>是位于函数开始位置的一个字符串，
解释了函数的接口（“doc”是“documentation”的缩写）。 下面是一个例子：</p>
<pre>def polyline(t, n, length, angle):
    """Draws n line segments with the given length and
    angle (in degrees) between them.  t is a turtle.
    """
    for i in range(n):
        t.fd(length)
        t.lt(angle)
</pre>
<p>按照惯例，所有的文档字符串都是三重引号（triple-quoted）字符串，也被称为多行字符串，
因为三重引号允许字符串超过一行。</p>
<p>它很简要（terse），但是包括了他人使用此函数时需要了解的关键信息。
它扼要地说明该函数做什么（不介绍背后的具体细节）。
它解释了每个形参对函数的行为有什么影响，以及每个形参应有的类型
（如果它不明显的话）。</p>
<p>写这种文档是接口设计中很重要的一部分。 一个设计良好的接口应该很容易解释，
如果你很难解释你的某个函数，那么你的接口也许还有改进空间。</p>
<a name="user-content-id10"></a>
<h2><a id="user-content-调试" class="anchor" href="#调试" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>调试</h2>
<p>接口就像是函数和调用者之间的合同。
调用者同意提供合适的参数，函数同意完成相应的工作。</p>
<p>例如，<code>polyline</code> 函数需要4个实参：<code>t</code> 必须是一个 <code>Turtle</code> ；
<code>n</code> 必须是一个整型数； <code>length</code> 应该是一个正数；
<code>angle</code> 必须是一个数，单位是度数。</p>
<p>这些要求被称作<strong>先决条件（preconditions）</strong>，
因为它们应当在函数开始执行之前成立（true）。
相反，函数结束时的条件是<strong>后置条件（postconditions）</strong>。
后置条件包括函数预期的效果（如画线段）以及任何其他附带效果
（如移动 <code>Turtle</code> 或者做其它改变）。</p>
<p>先决条件由调用者负责满足。如果调用者违反一个（已经充分记录文档的！）
先决条件，导致函数没有正确工作，则故障（bug）出现在调用者一方，而不是函数。</p>
<p>如果满足了先决条件，没有满足后置条件，故障就在函数一方。如果你的先决条件和后置条件都很清楚，将有助于调试。</p>
<a name="user-content-id11"></a>
<h2><a id="user-content-术语表" class="anchor" href="#术语表" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>术语表</h2>
<dl>
<dt>方法（method）：</dt>
<dd>与对象相关联的函数，并使用点标记法（dot notation）调用。</dd>
<dt>循环（loop）：</dt>
<dd>程序中能够重复执行的那部分代码。</dd>
<dt>封装（encapsulation）：</dt>
<dd>将一个语句序列转换成函数定义的过程。</dd>
<dt>泛化（generalization）：</dt>
<dd>使用某种可以算是比较通用的东西（像变量和形参），替代某些没必要那么具体的东西（像一个数字）的过程。</dd>
<dt>关键字实参（keyword argument）：</dt>
<dd>包括了形参名称作为“关键字”的实参。</dd>
<dt>接口（interface）：</dt>
<dd>对如何使用一个函数的描述，包括函数名、参数说明和返回值。</dd>
<dt>重构（refactoring）：</dt>
<dd>修改一个正常运行的函数，改善函数接口及其他方面代码质量的过程。</dd>
<dt>开发计划（development plan）：</dt>
<dd>编写程序的一种过程。</dd>
<dt>文档字符串（docstring）：</dt>
<dd>出现在函数定义顶部的一个字符串，用于记录函数的接口。</dd>
<dt>先决条件（preconditions）：</dt>
<dd>在函数运行之前，调用者应该满足的要求。
ends.</dd>
<dt>后置条件（postconditions）：</dt>
<dd>函数终止之前应该满足的条件。</dd>
</dl>
<a name="user-content-id12"></a>
<h2><a id="user-content-练习题" class="anchor" href="#练习题" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>练习题</h2>
<p>习题 4-1.</p>
<p>可从<a href="http://thinkpython2.com/code/polygon.py">http://thinkpython2.com/code/polygon.py</a> 下载本章的代码。</p>
<ol>
<li>画一个执行 <code>circle(bob, radius)</code> 时的堆栈图（stack diagram），说明程序的各个状态。你可以手动进行计算，也可以在代码中加入打印语句。</li>
<li>“重构”一节中给出的 <code>arc</code> 函数版本并不太精确，因为圆形的线性近似（linear approximation）永远处在真正的圆形之外。因此，<code>Turtle</code> 总是和正确的终点相差几个像素。我的答案中展示了降低这个错误影响的一种方法。阅读其中的代码，看看你是否能够理解。如果你画一个堆栈图的话，你可能会更容易明白背后的原理。</li>
</ol>
<p>习题 4-2.</p>
<div>
<a href="/bingjin/ThinkPython2-CN/blob/master/source/figs/flowers.png" target="_blank"><img alt="使用Turtle绘制的花朵。" src="/bingjin/ThinkPython2-CN/raw/master/source/figs/flowers.png" style="max-width:100%;"></a>
<p>图4-1：使用Turtle绘制的花朵。</p>
</div>
<p>编写比较通用的一个可以画出像图4-1中那样花朵的函数集。</p>
<p>答案： <a href="http://thinkpython2.com/code/flower.py">http://thinkpython2.com/code/flower.py</a> ，还要求使用这个模块
<a href="http://thinkpython2.com/code/polygon.py">http://thinkpython2.com/code/polygon.py</a>.</p>
<p>习题 4-3.</p>
<div>
<a href="/bingjin/ThinkPython2-CN/blob/master/source/figs/pies.png" target="_blank"><img alt="图4-2：使用Turtle画的饼状图。" src="/bingjin/ThinkPython2-CN/raw/master/source/figs/pies.png" style="max-width:100%;"></a>
<p>图4-2：使用Turtle画的饼状图。</p>
</div>
<p>编写比较通用的一个可以画出图4-2中那样图形的函数集，。</p>
<p>答案： <a href="http://thinkpython2.com/code/pie.py">http://thinkpython2.com/code/pie.py</a> 。</p>
<p>习题 4-4.</p>
<p>字母表中的字母可以由少量基本元素构成，例如竖线和横线，以及一些曲线。
设计一种可用由最少的基本元素绘制出的字母表，然后编写能画出各个字母的函数。</p>
<p>你应该为每个字母写一个函数，起名为<code>draw_a</code>，<code>draw_b</code>等等，
然后将你的函数放在一个名为 <code>letters.py</code> 的文件里。
你可以从<a href="http://thinkpython2.com/code/typewriter.py">http://thinkpython2.com/code/typewriter.py</a>
下载一个“海龟打字员”来帮你测试代码。</p>
<p>你可以在 <a href="http://thinkpython2.com/code/letters.py">http://thinkpython2.com/code/letters.py</a> 中找到答案；这个解法还要求使用 <a href="http://thinkpython2.com/code/polygon.py">http://thinkpython2.com/code/polygon.py</a> 。</p>
<p>习题 4-5.</p>
<p>前往<a href="http://en.wikipedia.org/wiki/Spiral">http://en.wikipedia.org/wiki/Spiral</a> 阅读螺线（spiral）的相关知识；
然后编写一个绘制阿基米德螺线（或者其他种类的螺线）的程序。</p>
<p>答案：<a href="http://thinkpython2.com/code/spiral.py">http://thinkpython2.com/code/spiral.py</a> 。</p>
<p><strong>贡献者</strong></p>
<ol>
<li>翻译：<a href="https://github.com/bingjin">@bingjin</a></li>
<li>校对：<a href="https://github.com/bingjin">@bingjin</a></li>
<li>参考：<a href="https://github.com/carfly">@carfly</a></li>
</ol>

</article>
  </div>

</div>

<button type="button" data-facebox="#jump-to-line" data-facebox-class="linejump" data-hotkey="l" class="hidden">Jump to Line</button>
<div id="jump-to-line" style="display:none">
  <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="" class="js-jump-to-line-form" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
    <input class="form-control linejump-input js-jump-to-line-field" type="text" placeholder="Jump to line&hellip;" aria-label="Jump to line" autofocus>
    <button type="submit" class="btn">Go</button>
</form></div>

  </div>
  <div class="modal-backdrop"></div>
</div>


    </div>
  </div>

    </div>

        <div class="container site-footer-container">
  <div class="site-footer" role="contentinfo">
    <ul class="site-footer-links right">
        <li><a href="https://status.github.com/" data-ga-click="Footer, go to status, text:status">Status</a></li>
      <li><a href="https://developer.github.com" data-ga-click="Footer, go to api, text:api">API</a></li>
      <li><a href="https://training.github.com" data-ga-click="Footer, go to training, text:training">Training</a></li>
      <li><a href="https://shop.github.com" data-ga-click="Footer, go to shop, text:shop">Shop</a></li>
        <li><a href="https://github.com/blog" data-ga-click="Footer, go to blog, text:blog">Blog</a></li>
        <li><a href="https://github.com/about" data-ga-click="Footer, go to about, text:about">About</a></li>

    </ul>

    <a href="https://github.com" aria-label="Homepage" class="site-footer-mark">
      <svg aria-hidden="true" class="octicon octicon-mark-github" height="24" role="img" title="GitHub " version="1.1" viewBox="0 0 16 16" width="24"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59 0.4 0.07 0.55-0.17 0.55-0.38 0-0.19-0.01-0.82-0.01-1.49-2.01 0.37-2.53-0.49-2.69-0.94-0.09-0.23-0.48-0.94-0.82-1.13-0.28-0.15-0.68-0.52-0.01-0.53 0.63-0.01 1.08 0.58 1.23 0.82 0.72 1.21 1.87 0.87 2.33 0.66 0.07-0.52 0.28-0.87 0.51-1.07-1.78-0.2-3.64-0.89-3.64-3.95 0-0.87 0.31-1.59 0.82-2.15-0.08-0.2-0.36-1.02 0.08-2.12 0 0 0.67-0.21 2.2 0.82 0.64-0.18 1.32-0.27 2-0.27 0.68 0 1.36 0.09 2 0.27 1.53-1.04 2.2-0.82 2.2-0.82 0.44 1.1 0.16 1.92 0.08 2.12 0.51 0.56 0.82 1.27 0.82 2.15 0 3.07-1.87 3.75-3.65 3.95 0.29 0.25 0.54 0.73 0.54 1.48 0 1.07-0.01 1.93-0.01 2.2 0 0.21 0.15 0.46 0.55 0.38C13.71 14.53 16 11.53 16 8 16 3.58 12.42 0 8 0z"></path></svg>
</a>
    <ul class="site-footer-links">
      <li>&copy; 2016 <span title="0.09228s from github-fe138-cp1-prd.iad.github.net">GitHub</span>, Inc.</li>
        <li><a href="https://github.com/site/terms" data-ga-click="Footer, go to terms, text:terms">Terms</a></li>
        <li><a href="https://github.com/site/privacy" data-ga-click="Footer, go to privacy, text:privacy">Privacy</a></li>
        <li><a href="https://github.com/security" data-ga-click="Footer, go to security, text:security">Security</a></li>
        <li><a href="https://github.com/contact" data-ga-click="Footer, go to contact, text:contact">Contact</a></li>
        <li><a href="https://help.github.com" data-ga-click="Footer, go to help, text:help">Help</a></li>
    </ul>
  </div>
</div>



    
    
    

    <div id="ajax-error-message" class="ajax-error-message flash flash-error">
      <svg aria-hidden="true" class="octicon octicon-alert" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M15.72 12.5l-6.85-11.98C8.69 0.21 8.36 0.02 8 0.02s-0.69 0.19-0.87 0.5l-6.85 11.98c-0.18 0.31-0.18 0.69 0 1C0.47 13.81 0.8 14 1.15 14h13.7c0.36 0 0.69-0.19 0.86-0.5S15.89 12.81 15.72 12.5zM9 12H7V10h2V12zM9 9H7V5h2V9z"></path></svg>
      <button type="button" class="flash-close js-flash-close js-ajax-error-dismiss" aria-label="Dismiss error">
        <svg aria-hidden="true" class="octicon octicon-x" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M7.48 8l3.75 3.75-1.48 1.48-3.75-3.75-3.75 3.75-1.48-1.48 3.75-3.75L0.77 4.25l1.48-1.48 3.75 3.75 3.75-3.75 1.48 1.48-3.75 3.75z"></path></svg>
      </button>
      Something went wrong with that request. Please try again.
    </div>


      
      <script crossorigin="anonymous" integrity="sha256-IOKDFpHJuwpNwb13hSn8HBbsjIoksy2ZZPmEdy0usks=" src="https://assets-cdn.github.com/assets/frameworks-20e2831691c9bb0a4dc1bd778529fc1c16ec8c8a24b32d9964f984772d2eb24b.js"></script>
      <script async="async" crossorigin="anonymous" integrity="sha256-qxCGlIo75SgAFxAIC6F+SXXds2qTeat93f2wNwZHt8E=" src="https://assets-cdn.github.com/assets/github-ab1086948a3be528001710080ba17e4975ddb36a9379ab7dddfdb0370647b7c1.js"></script>
      
      
      
      
    <div class="js-stale-session-flash stale-session-flash flash flash-warn flash-banner hidden">
      <svg aria-hidden="true" class="octicon octicon-alert" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M15.72 12.5l-6.85-11.98C8.69 0.21 8.36 0.02 8 0.02s-0.69 0.19-0.87 0.5l-6.85 11.98c-0.18 0.31-0.18 0.69 0 1C0.47 13.81 0.8 14 1.15 14h13.7c0.36 0 0.69-0.19 0.86-0.5S15.89 12.81 15.72 12.5zM9 12H7V10h2V12zM9 9H7V5h2V9z"></path></svg>
      <span class="signed-in-tab-flash">You signed in with another tab or window. <a href="">Reload</a> to refresh your session.</span>
      <span class="signed-out-tab-flash">You signed out in another tab or window. <a href="">Reload</a> to refresh your session.</span>
    </div>
    <div class="facebox" id="facebox" style="display:none;">
  <div class="facebox-popup">
    <div class="facebox-content" role="dialog" aria-labelledby="facebox-header" aria-describedby="facebox-description">
    </div>
    <button type="button" class="facebox-close js-facebox-close" aria-label="Close modal">
      <svg aria-hidden="true" class="octicon octicon-x" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M7.48 8l3.75 3.75-1.48 1.48-3.75-3.75-3.75 3.75-1.48-1.48 3.75-3.75L0.77 4.25l1.48-1.48 3.75 3.75 3.75-3.75 1.48 1.48-3.75 3.75z"></path></svg>
    </button>
  </div>
</div>

  </body>
</html>

