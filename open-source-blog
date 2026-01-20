import React, { useState, useMemo } from 'react';
import { Search, Calendar, User, Tag, Heart, MessageCircle, Eye, TrendingUp } from 'lucide-react';

// Dummy data generator
const generateBlogPosts = () => {
  const titles = [
    'Getting Started with React Hooks',
    'The Future of Web Development',
    'Understanding JavaScript Closures',
    'CSS Grid vs Flexbox: A Complete Guide',
    'Building Scalable Node.js Applications',
    'Machine Learning for Beginners',
    'The Art of Writing Clean Code',
    'Mastering TypeScript in 2025',
    'Docker and Kubernetes Explained',
    'Web Accessibility Best Practices',
    'GraphQL vs REST APIs',
    'Introduction to Microservices',
    'Modern JavaScript Features You Should Know',
    'Responsive Design Patterns',
    'Testing Strategies for React Apps',
    'Database Design Fundamentals',
    'Security Best Practices for Web Apps',
    'Performance Optimization Techniques',
    'Introduction to Serverless Architecture',
    'Git Workflow and Best Practices',
    'UI/UX Design Principles',
    'Building Progressive Web Apps',
    'Understanding Async/Await',
    'The Power of CSS Variables',
    'State Management in React'
  ];

  const authors = [
    'Sarah Johnson', 'Michael Chen', 'Emma Williams', 'David Martinez',
    'Lisa Anderson', 'James Taylor', 'Maria Garcia', 'Robert Kim'
  ];

  const tags = [
    'JavaScript', 'React', 'CSS', 'Node.js', 'TypeScript',
    'Web Development', 'Tutorial', 'Best Practices', 'Performance',
    'Security', 'Design', 'DevOps', 'Database', 'Testing'
  ];

  const excerpts = [
    'Learn the fundamentals and advanced concepts that will help you become a better developer.',
    'Explore the latest trends and technologies shaping the future of web development.',
    'A comprehensive guide to understanding and implementing these important concepts.',
    'Dive deep into the best practices and common pitfalls you should avoid.',
    'Discover practical tips and techniques used by industry professionals.',
    'Everything you need to know to get started with this powerful technology.',
    'Master these essential skills that every developer should have in their toolkit.',
    'A step-by-step tutorial with real-world examples and code snippets.'
  ];

  return titles.map((title, i) => {
    const postTags = Array.from(
      { length: Math.floor(Math.random() * 3) + 2 },
      () => tags[Math.floor(Math.random() * tags.length)]
    ).filter((tag, idx, arr) => arr.indexOf(tag) === idx);

    const daysAgo = Math.floor(Math.random() * 90);
    const date = new Date();
    date.setDate(date.getDate() - daysAgo);

    return {
      id: i + 1,
      title,
      author: authors[Math.floor(Math.random() * authors.length)],
      excerpt: excerpts[Math.floor(Math.random() * excerpts.length)],
      date: date.toISOString().split('T')[0],
      tags: postTags,
      likes: Math.floor(Math.random() * 500),
      comments: Math.floor(Math.random() * 50),
      views: Math.floor(Math.random() * 5000) + 100,
      readTime: Math.floor(Math.random() * 10) + 3,
      featured: Math.random() > 0.8
    };
  });
};

const BlogPlatform = () => {
  const [posts] = useState(generateBlogPosts());
  const [searchTerm, setSearchTerm] = useState('');
  const [selectedTag, setSelectedTag] = useState('All');
  const [sortBy, setSortBy] = useState('date');
  const [selectedPost, setSelectedPost] = useState(null);

  const allTags = ['All', ...new Set(posts.flatMap(p => p.tags))].sort();

  const filteredPosts = useMemo(() => {
    let filtered = posts.filter(p => 
      (p.title.toLowerCase().includes(searchTerm.toLowerCase()) ||
       p.author.toLowerCase().includes(searchTerm.toLowerCase())) &&
      (selectedTag === 'All' || p.tags.includes(selectedTag))
    );

    return filtered.sort((a, b) => {
      if (sortBy === 'date') return new Date(b.date) - new Date(a.date);
      if (sortBy === 'popular') return b.views - a.views;
      if (sortBy === 'likes') return b.likes - a.likes;
      return 0;
    });
  }, [posts, searchTerm, selectedTag, sortBy]);

  const stats = useMemo(() => ({
    totalPosts: posts.length,
    totalViews: posts.reduce((sum, p) => sum + p.views, 0),
    totalLikes: posts.reduce((sum, p) => sum + p.likes, 0),
    featuredPosts: posts.filter(p => p.featured).length
  }), [posts]);

  if (selectedPost) {
    return (
      <div className="min-h-screen bg-gray-50">
        <div className="max-w-4xl mx-auto px-6 py-8">
          <button
            onClick={() => setSelectedPost(null)}
            className="mb-6 text-blue-600 hover:text-blue-700 font-medium"
          >
            ← Back to all posts
          </button>
          
          <article className="bg-white rounded-lg shadow-lg p-8">
            {selectedPost.featured && (
              <span className="inline-block px-3 py-1 bg-yellow-100 text-yellow-800 text-xs font-semibold rounded-full mb-4">
                Featured Post
              </span>
            )}
            
            <h1 className="text-4xl font-bold text-gray-900 mb-4">{selectedPost.title}</h1>
            
            <div className="flex flex-wrap items-center gap-4 text-sm text-gray-600 mb-6 pb-6 border-b">
              <div className="flex items-center gap-2">
                <User className="w-4 h-4" />
                <span>{selectedPost.author}</span>
              </div>
              <div className="flex items-center gap-2">
                <Calendar className="w-4 h-4" />
                <span>{new Date(selectedPost.date).toLocaleDateString('en-US', { year: 'numeric', month: 'long', day: 'numeric' })}</span>
              </div>
              <div className="flex items-center gap-2">
                <Eye className="w-4 h-4" />
                <span>{selectedPost.views.toLocaleString()} views</span>
              </div>
              <span>{selectedPost.readTime} min read</span>
            </div>

            <div className="prose max-w-none mb-6">
              <p className="text-lg text-gray-700 leading-relaxed mb-4">{selectedPost.excerpt}</p>
              <p className="text-gray-700 leading-relaxed mb-4">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
              </p>
              <h2 className="text-2xl font-bold text-gray-900 mt-6 mb-3">Key Takeaways</h2>
              <p className="text-gray-700 leading-relaxed mb-4">
                Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
              </p>
              <p className="text-gray-700 leading-relaxed">
                Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo.
              </p>
            </div>

            <div className="flex flex-wrap gap-2 mb-6">
              {selectedPost.tags.map(tag => (
                <span key={tag} className="px-3 py-1 bg-blue-100 text-blue-700 text-sm rounded-full">
                  {tag}
                </span>
              ))}
            </div>

            <div className="flex items-center gap-6 pt-6 border-t">
              <button className="flex items-center gap-2 text-gray-600 hover:text-red-500 transition-colors">
                <Heart className="w-5 h-5" />
                <span>{selectedPost.likes}</span>
              </button>
              <button className="flex items-center gap-2 text-gray-600 hover:text-blue-500 transition-colors">
                <MessageCircle className="w-5 h-5" />
                <span>{selectedPost.comments}</span>
              </button>
            </div>
          </article>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gray-50 p-6">
      <div className="max-w-7xl mx-auto">
        <div className="mb-8">
          <h1 className="text-4xl font-bold text-gray-900 mb-2">Tech Blog</h1>
          <p className="text-gray-600">Explore articles, tutorials, and insights from our community</p>
        </div>

        {/* Stats Cards */}
        <div className="grid grid-cols-1 md:grid-cols-4 gap-4 mb-6">
          <div className="bg-white rounded-lg shadow p-6">
            <div className="flex items-center justify-between">
              <div>
                <p className="text-sm text-gray-600">Total Posts</p>
                <p className="text-2xl font-bold text-gray-900">{stats.totalPosts}</p>
              </div>
              <TrendingUp className="w-8 h-8 text-blue-500" />
            </div>
          </div>
          <div className="bg-white rounded-lg shadow p-6">
            <div className="flex items-center justify-between">
              <div>
                <p className="text-sm text-gray-600">Total Views</p>
                <p className="text-2xl font-bold text-gray-900">{stats.totalViews.toLocaleString()}</p>
              </div>
              <Eye className="w-8 h-8 text-green-500" />
            </div>
          </div>
          <div className="bg-white rounded-lg shadow p-6">
            <div className="flex items-center justify-between">
              <div>
                <p className="text-sm text-gray-600">Total Likes</p>
                <p className="text-2xl font-bold text-gray-900">{stats.totalLikes.toLocaleString()}</p>
              </div>
              <Heart className="w-8 h-8 text-red-500" />
            </div>
          </div>
          <div className="bg-white rounded-lg shadow p-6">
            <div className="flex items-center justify-between">
              <div>
                <p className="text-sm text-gray-600">Featured</p>
                <p className="text-2xl font-bold text-gray-900">{stats.featuredPosts}</p>
              </div>
              <Tag className="w-8 h-8 text-purple-500" />
            </div>
          </div>
        </div>

        {/* Filters */}
        <div className="bg-white rounded-lg shadow p-6 mb-6">
          <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
            <div className="relative">
              <Search className="absolute left-3 top-3 w-5 h-5 text-gray-400" />
              <input
                type="text"
                placeholder="Search posts or authors..."
                value={searchTerm}
                onChange={(e) => setSearchTerm(e.target.value)}
                className="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
              />
            </div>
            <div className="relative">
              <Tag className="absolute left-3 top-3 w-5 h-5 text-gray-400" />
              <select
                value={selectedTag}
                onChange={(e) => setSelectedTag(e.target.value)}
                className="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent appearance-none"
              >
                {allTags.map(tag => (
                  <option key={tag} value={tag}>{tag}</option>
                ))}
              </select>
            </div>
            <select
              value={sortBy}
              onChange={(e) => setSortBy(e.target.value)}
              className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
            >
              <option value="date">Latest First</option>
              <option value="popular">Most Popular</option>
              <option value="likes">Most Liked</option>
            </select>
          </div>
        </div>

        {/* Blog Posts Grid */}
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          {filteredPosts.map(post => (
            <article
              key={post.id}
              className="bg-white rounded-lg shadow hover:shadow-lg transition-shadow cursor-pointer overflow-hidden"
              onClick={() => setSelectedPost(post)}
            >
              <div className="p-6">
                {post.featured && (
                  <span className="inline-block px-2 py-1 bg-yellow-100 text-yellow-800 text-xs font-semibold rounded-full mb-3">
                    Featured
                  </span>
                )}
                
                <h2 className="text-xl font-bold text-gray-900 mb-3 line-clamp-2 hover:text-blue-600 transition-colors">
                  {post.title}
                </h2>
                
                <p className="text-gray-600 text-sm mb-4 line-clamp-3">{post.excerpt}</p>
                
                <div className="flex flex-wrap gap-2 mb-4">
                  {post.tags.slice(0, 2).map(tag => (
                    <span key={tag} className="px-2 py-1 bg-blue-50 text-blue-600 text-xs rounded-full">
                      {tag}
                    </span>
                  ))}
                </div>
                
                <div className="flex items-center justify-between text-sm text-gray-500 mb-4">
                  <div className="flex items-center gap-2">
                    <User className="w-4 h-4" />
                    <span>{post.author}</span>
                  </div>
                  <span>{post.readTime} min read</span>
                </div>
                
                <div className="flex items-center gap-2 text-sm text-gray-500 border-t pt-4">
                  <Calendar className="w-4 h-4" />
                  <span>{new Date(post.date).toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' })}</span>
                </div>
              </div>
              
              <div className="flex items-center gap-4 px-6 py-3 bg-gray-50 border-t">
                <div className="flex items-center gap-1 text-gray-600">
                  <Heart className="w-4 h-4" />
                  <span className="text-sm">{post.likes}</span>
                </div>
                <div className="flex items-center gap-1 text-gray-600">
                  <MessageCircle className="w-4 h-4" />
                  <span className="text-sm">{post.comments}</span>
                </div>
                <div className="flex items-center gap-1 text-gray-600">
                  <Eye className="w-4 h-4" />
                  <span className="text-sm">{post.views.toLocaleString()}</span>
                </div>
              </div>
            </article>
          ))}
        </div>

        {filteredPosts.length === 0 && (
          <div className="text-center py-12 bg-white rounded-lg shadow">
            <p className="text-gray-500">No posts found matching your criteria</p>
          </div>
        )}
      </div>
    </div>
  );
};

export default BlogPlatform;
