# Chart Template Guide

This document provides instructions for creating new chart pages in the yoDEV Charts gallery.

## File Structure

Each chart is a standalone HTML file located in the `charts/` directory with the following components:

1. HTML file with embedded React/Recharts code
2. SVG preview image for social sharing
3. OpenGraph meta tags for link previews

## HTML Chart Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[Chart Title] - yoDEV Charts</title>

    <!-- OpenGraph Meta Tags for Discourse -->
    <meta property="og:title" content="[Chart Title]">
    <meta property="og:description" content="[Chart Description]">
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://inova-charts.netlify.app/charts/[filename].html">
    <meta property="og:site_name" content="yoDEV Charts">
    <meta property="og:image" content="https://inova-charts.netlify.app/charts/preview-[filename].svg">
    <meta property="og:image:width" content="1200">
    <meta property="og:image:height" content="630">

    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="m-0 p-0">
    <div id="root"></div>

    <script type="module">
        import React from 'https://esm.sh/react@18';
        import ReactDOM from 'https://esm.sh/react-dom@18/client';
        import { BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } from 'https://esm.sh/recharts@2.12.7';

        window.React = React;
        window.ReactDOM = ReactDOM;

        function ChartComponent() {
          const data = [
            // Your chart data here
          ];

          return React.createElement('div', { className: "w-full h-full min-h-screen p-4 sm:p-8 bg-gradient-to-br from-slate-50 to-slate-100" },
            React.createElement('div', { className: "max-w-5xl mx-auto bg-white rounded-xl shadow-lg p-4 sm:p-8" },
              // Back to gallery link
              React.createElement('div', { className: "mb-4" },
                React.createElement('a', {
                  href: '../index.html',
                  className: "inline-flex items-center text-blue-600 hover:text-blue-700 font-medium text-sm mb-4"
                },
                  '← Back to Gallery'
                )
              ),
              // Chart title
              React.createElement('h2', { className: "text-2xl sm:text-3xl font-bold text-slate-800 mb-2" },
                '[Chart Title]'
              ),
              // Chart description
              React.createElement('p', { className: "text-slate-600 mb-6 text-sm sm:text-base" },
                '[Chart subtitle or description]'
              ),

              // Recharts component
              React.createElement(ResponsiveContainer, { width: "100%", height: 450 },
                React.createElement(BarChart, { data: data, margin: { top: 20, right: 30, left: 20, bottom: 80 } },
                  React.createElement(CartesianGrid, { strokeDasharray: "3 3", stroke: "#e2e8f0" }),
                  React.createElement(XAxis, { dataKey: "name", tick: { fill: '#475569' } }),
                  React.createElement(YAxis, { tick: { fill: '#475569' } }),
                  React.createElement(Tooltip, {
                    contentStyle: {
                      backgroundColor: '#fff',
                      border: '1px solid #e2e8f0',
                      borderRadius: '8px',
                      boxShadow: '0 4px 6px -1px rgb(0 0 0 / 0.1)'
                    }
                  }),
                  React.createElement(Bar, { dataKey: "value", fill: "#3b82f6", radius: [8, 8, 0, 0] })
                )
              ),

              // Additional context or notes
              React.createElement('div', { className: "mt-6 p-4 bg-blue-50 rounded-lg border border-blue-200" },
                React.createElement('p', { className: "text-sm text-slate-700" },
                  '[Key insights or notes about the chart]'
                )
              ),

              // Sources
              React.createElement('div', { className: "mt-4 text-xs text-slate-500" },
                'Sources: [List your data sources]'
              )
            )
          );
        }

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(React.createElement(ChartComponent));
    </script>
</body>
</html>
```

## Preview Image Template (SVG)

Create a `preview-[filename].svg` file with dimensions 1200x630:

```xml
<svg width="1200" height="630" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <linearGradient id="grad" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" style="stop-color:#3b82f6;stop-opacity:1" />
      <stop offset="100%" style="stop-color:#1e40af;stop-opacity:1" />
    </linearGradient>
  </defs>
  <rect width="1200" height="630" fill="url(#grad)"/>
  <text x="600" y="280" font-family="Arial, sans-serif" font-size="64" font-weight="bold" fill="white" text-anchor="middle">
    [Chart Title]
  </text>
  <text x="600" y="350" font-family="Arial, sans-serif" font-size="32" fill="#e0e7ff" text-anchor="middle">
    [Subtitle]
  </text>
</svg>
```

## Important Technical Details

### ESM Module Imports

**Always use ESM imports** (not UMD):
```javascript
import React from 'https://esm.sh/react@18';
import ReactDOM from 'https://esm.sh/react-dom@18/client';
import { ComponentName } from 'https://esm.sh/recharts@2.12.7';
```

**Required**: Export to window for Tailwind CDN compatibility:
```javascript
window.React = React;
window.ReactDOM = ReactDOM;
```

### Available Recharts Components

Import only what you need from Recharts:

**Chart Types:**
- `BarChart` - Bar charts
- `LineChart` - Line charts
- `PieChart` - Pie charts
- `AreaChart` - Area charts
- `ComposedChart` - Mixed chart types
- `ScatterChart` - Scatter plots
- `RadarChart` - Radar charts

**Chart Elements:**
- `Bar`, `Line`, `Area`, `Pie`, `Scatter`, `Radar` - Data series
- `XAxis`, `YAxis` - Axes
- `CartesianGrid` - Grid lines
- `Tooltip` - Hover tooltips
- `Legend` - Chart legend
- `ResponsiveContainer` - Makes chart responsive
- `Cell` - Individual bar/pie colors
- `ReferenceLine` - Reference lines

### React.createElement Syntax

Since we're not using JSX, use `React.createElement`:

```javascript
React.createElement(component, props, ...children)
```

Examples:
```javascript
// Single child
React.createElement('div', { className: "text-xl" }, 'Hello')

// Multiple children
React.createElement('div', { className: "container" },
  React.createElement('h1', null, 'Title'),
  React.createElement('p', null, 'Text')
)

// Recharts component
React.createElement(BarChart, { data: data, width: 500, height: 300 },
  React.createElement(Bar, { dataKey: "value", fill: "#3b82f6" })
)
```

## Styling Guidelines

### Tailwind Classes

Common utility classes used:
- Layout: `w-full`, `h-full`, `min-h-screen`, `max-w-5xl`, `mx-auto`
- Spacing: `p-4`, `p-8`, `m-4`, `mb-6`, `mt-4`
- Colors: `bg-white`, `bg-slate-50`, `text-slate-800`, `text-blue-600`
- Effects: `rounded-xl`, `shadow-lg`, `hover:text-blue-700`
- Gradients: `bg-gradient-to-br from-slate-50 to-slate-100`

### Color Schemes

Use consistent colors:
- Primary blue: `#3b82f6`
- Purple: `#8b5cf6`
- Green: `#10b981`
- Red: `#ef4444`
- Slate text: `#475569`, `#64748b`

## Adding to Gallery

After creating a new chart, add it to `index.html`:

```javascript
{
  title: '[Chart Title]',
  description: '[Brief description]',
  date: 'Month Year',
  link: 'charts/[filename].html',
  tags: ['tag1', 'tag2']
}
```

## Deployment

1. Commit changes: `git add . && git commit -m "Add [chart name]"`
2. Push to GitHub: `git push`
3. Netlify auto-deploys from the main branch
4. Clear browser cache if needed (Cmd+Shift+R)

## OpenGraph Best Practices

- **og:title**: 40-60 characters, descriptive
- **og:description**: 150-160 characters, compelling summary
- **og:image**: Always 1200x630px for best display
- **og:url**: Full absolute URL to the chart page
- **og:site_name**: "yoDEV Charts" for branding

## Discourse Integration

To embed in Discourse posts:
1. Paste the full chart URL on its own line
2. Discourse will automatically create a "onebox" preview
3. Preview shows: title, description, and thumbnail image
4. Clicking opens the interactive chart

## Troubleshooting

### Charts not rendering
- Check browser console for errors
- Verify ESM imports are correct
- Ensure `window.React` and `window.ReactDOM` are set
- Hard refresh to clear cache (Cmd+Shift+R)

### No preview in Discourse
- Verify all OpenGraph meta tags are present
- Check og:image URL is accessible
- Try opening in incognito to test without cache
- Some Discourse instances may have domain allowlists

### Styling issues
- Tailwind CDN loads automatically
- Use className (not class) for React elements
- Check responsive classes: `text-sm sm:text-base`

## Examples

See existing charts in `charts/` directory:
- `global-equity-2025.html` - Bar chart with colored bars
- `april-volatility-2025.html` - Line chart with area fill
- `annual-returns-2023-2025.html` - Grouped bar chart with legend
