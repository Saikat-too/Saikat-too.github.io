---
layout: default
title: "💭 Thoughts & Reflections"
description: "A collection of my random thoughts, beliefs, philosophy, and musings on life"
permalink: /thoughts/
---

<div class="thoughts-container">
  <header class="thoughts-header">
    <h1 class="thoughts-title">
      <span class="thoughts-emoji">💭</span>
      Thoughts & Reflections
    </h1>
    <p class="thoughts-subtitle">
      Welcome to my digital mind garden — where I share random thoughts, beliefs, philosophy, and reflections on life.
    </p>
  </header>

  {% if site.thoughts.size > 0 %}
    <div class="thoughts-stats">
      <div class="stat-item">
        <span class="stat-number">{{ site.thoughts | size }}</span>
        <span class="stat-label">Total Thoughts</span>
      </div>
      <div class="stat-item">
        <span class="stat-number">{{ site.thoughts | map: 'categories' | join: ',' | split: ',' | uniq | size }}</span>
        <span class="stat-label">Categories</span>
      </div>
      <div class="stat-item">
        <span class="stat-number">{{ site.thoughts | map: 'content' | join: ' ' | number_of_words }}</span>
        <span class="stat-label">Words Written</span>
      </div>
    </div>
  {% else %}
    <div class="empty-state-banner">
      <div class="empty-banner-icon">🌱</div>
      <div class="empty-banner-text">
        <h3>Mind garden awaits</h3>
        <p>Start planting first thoughts</p>
      </div>
    </div>
  {% endif %}

  {% if site.thoughts.size > 0 %}
    <div class="thoughts-grid">
      {% assign sorted_thoughts = site.thoughts | sort: 'last_modified_at' | reverse %}
      {% for thought in sorted_thoughts %}
        <article class="thought-card">
          <div class="thought-meta">
            <div class="thought-date">
              <svg class="date-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <circle cx="12" cy="12" r="10"></circle>
                <polyline points="12,6 12,12 16,14"></polyline>
              </svg>
              <time datetime="{{ thought.last_modified_at | date: '%Y-%m-%d' }}">
                {{ thought.last_modified_at | date: "%B %d, %Y" }}
              </time>
            </div>

            <div class="thought-reading-time">
              <svg class="reading-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"></path>
                <path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"></path>
              </svg>
              {% capture words %}{{ thought.content | number_of_words }}{% endcapture %}
              {% unless words contains '-' %}
                {{ words | plus: 0 | divided_by: 250 | append: ' min read' }}
              {% endunless %}
            </div>
          </div>

          <div class="thought-content">
            <h2 class="thought-title">
              <a href="{{ thought.url | relative_url }}" class="thought-link">
                {{ thought.title }}
              </a>
            </h2>

            <div class="thought-excerpt">
              {{ thought.excerpt | strip_html | truncatewords: 30 }}
            </div>

            <div class="thought-footer">
              {% if thought.categories.size > 0 %}
                <div class="thought-categories">
                  <svg class="category-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M20.59 13.41l-7.17 7.17a2 2 0 0 1-2.83 0L2 12V2h10l8.59 8.59a2 2 0 0 1 0 2.82z"></path>
                    <line x1="7" y1="7" x2="7.01" y2="7"></line>
                  </svg>
                  {% for category in thought.categories %}
                    <span class="category-tag">{{ category }}</span>
                  {% endfor %}
                </div>
              {% endif %}

              <a href="{{ thought.url | relative_url }}" class="read-more-link">
                Read more
                <svg class="arrow-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <line x1="7" y1="17" x2="17" y2="7"></line>
                  <polyline points="7,7 17,7 17,17"></polyline>
                </svg>
              </a>
            </div>
          </div>
        </article>
      {% endfor %}
    </div>
  {% else %}
    <div class="no-thoughts">
      <div class="no-thoughts-icon">💭</div>
      <h3>No thoughts captured yet</h3>
      <p>Ready for the first seeds of the wisdom?</p>
      <div class="getting-started">
        <h4>Ready to start?</h4>

      </div>
    </div>
  {% endif %}
</div>

<style>
  .thoughts-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  }

  .thoughts-header {
    text-align: center;
    margin-bottom: 3rem;
    padding: 2rem 0;
    border-bottom: 1px solid #e2e8f0;
  }

  .thoughts-title {
    font-size: 3rem;
    font-weight: 700;
    color: #1a202c;
    margin: 0 0 1rem 0;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
  }

  .thoughts-emoji {
    font-size: 2.5rem;
    animation: float 3s ease-in-out infinite;
  }

  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-10px); }
  }

  .thoughts-subtitle {
    font-size: 1.125rem;
    color: #64748b;
    max-width: 600px;
    margin: 0 auto;
    line-height: 1.6;
  }

  .thoughts-stats {
    display: flex;
    justify-content: center;
    gap: 3rem;
    margin-bottom: 3rem;
    padding: 2rem;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border-radius: 1rem;
    color: white;
  }

  .stat-item {
    text-align: center;
  }

  .stat-number {
    display: block;
    font-size: 2.5rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
  }

  .stat-label {
    font-size: 0.875rem;
    opacity: 0.9;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .thoughts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 2rem;
    margin-bottom: 3rem;
  }

  .thought-card {
    background: white;
    border-radius: 1rem;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
    overflow: hidden;
    transition: all 0.3s ease;
    border: 1px solid #e2e8f0;
  }

  .thought-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
  }

  .thought-meta {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 1.5rem;
    background: #f8fafc;
    border-bottom: 1px solid #e2e8f0;
  }

  .thought-date, .thought-reading-time {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.875rem;
    color: #64748b;
  }

  .date-icon, .reading-icon, .category-icon, .arrow-icon {
    width: 16px;
    height: 16px;
  }

  .thought-content {
    padding: 1.5rem;
  }

  .thought-title {
    margin: 0 0 1rem 0;
    font-size: 1.25rem;
    font-weight: 600;
  }

  .thought-link {
    color: #1a202c;
    text-decoration: none;
    transition: color 0.2s ease;
  }

  .thought-link:hover {
    color: #667eea;
  }

  .thought-excerpt {
    color: #64748b;
    line-height: 1.6;
    margin-bottom: 1.5rem;
  }

  .thought-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .thought-categories {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    flex-wrap: wrap;
  }

  .category-tag {
    background: #e2e8f0;
    color: #475569;
    padding: 0.25rem 0.75rem;
    border-radius: 9999px;
    font-size: 0.75rem;
    font-weight: 500;
  }

  .read-more-link {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    color: #667eea;
    text-decoration: none;
    font-weight: 500;
    font-size: 0.875rem;
    transition: color 0.2s ease;
  }

  .read-more-link:hover {
    color: #4c51bf;
  }

  .empty-state-banner {
    background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
    border-radius: 1rem;
    padding: 2rem;
    text-align: center;
    color: white;
    margin-bottom: 3rem;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1.5rem;
  }

  .empty-banner-icon {
    font-size: 3rem;
    animation: pulse 2s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.1); }
  }

  .empty-banner-text h3 {
    font-size: 1.5rem;
    margin: 0 0 0.5rem 0;
    font-weight: 600;
  }

  .empty-banner-text p {
    margin: 0;
    opacity: 0.9;
    font-size: 1rem;
  }

  .no-thoughts {
    text-align: center;
    padding: 4rem 2rem;
    color: #64748b;
    max-width: 600px;
    margin: 0 auto;
  }

  .no-thoughts-icon {
    font-size: 4rem;
    margin-bottom: 1.5rem;
    animation: float 3s ease-in-out infinite;
  }

  .no-thoughts h3 {
    font-size: 1.75rem;
    margin-bottom: 1rem;
    color: #374151;
    font-weight: 600;
  }

  .no-thoughts p {
    font-size: 1.125rem;
    margin-bottom: 2rem;
    line-height: 1.6;
  }

  .getting-started {
    background: #f8fafc;
    border-radius: 1rem;
    padding: 2rem;
    margin-top: 2rem;
    border: 1px solid #e2e8f0;
  }

  .getting-started h4 {
    color: #374151;
    margin-bottom: 1rem;
    font-size: 1.25rem;
    font-weight: 600;
  }



  @media (max-width: 768px) {
    .thoughts-container {
      padding: 1rem;
    }

    .thoughts-title {
      font-size: 2rem;
    }

    .thoughts-stats {
      flex-direction: column;
      gap: 1rem;
    }

    .empty-state-banner {
      flex-direction: column;
      gap: 1rem;
    }

    .empty-banner-icon {
      font-size: 2.5rem;
    }

    .thoughts-grid {
      grid-template-columns: 1fr;
    }

    .thought-footer {
      flex-direction: column;
      align-items: flex-start;
    }

    .getting-started {
      padding: 1.5rem;
    }
  }
</style>
