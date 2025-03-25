# Web-to-Doc: A Versatile Web Content Converter

Web-to-Doc is a powerful Python tool that crawls websites and converts their content into various document formats including PDF, HTML, Markdown, JSON, and DOCX. It's designed to help you create offline documentation, archive websites, or extract content for further processing.

## 📋 Features

- **Multiple Output Formats:** Convert websites to PDF, HTML, Markdown, JSON, or DOCX
- **Smart Crawling:** Automatically discover and follow links within the same documentation area
- **Content Filtering:** Include or exclude pages based on keywords or categories
- **Depth Control:** Limit crawling to a specific number of levels deep
- **Image Handling:** Processes and includes images in the output (with SVG support)
- **Interactive Mode:** Select which URLs to process through an interactive prompt
- **Sitemap Support:** Use website sitemaps for more efficient content discovery
- **Table of Contents:** Generate a navigable table of contents

## 🔧 Installation

1. Clone this repository or download the script files.

```bash
git clone https://github.com/coderplus007/website_documentation.git
cd website_documentation
```

2. Install the required dependencies:

```bash
pip install requests beautifulsoup4 reportlab Pillow
```

3. For additional formats, install the optional dependencies:

```bash
# For DOCX support
pip install python-docx

# For better XML handling (sitemaps)
pip install lxml
```

## 🚀 Usage

### Basic Usage

```bash
python web_to_doc.py --url https://docs.example.com/
```

This will crawl the website starting from the provided URL and generate a PDF file named `output.pdf` in the current directory.

### Specifying Output File

```bash
python web_to_doc.py --url https://docs.example.com/ --output documentation.pdf
```

### Changing Output Format

```bash
# Convert to HTML
python web_to_doc.py --url https://docs.example.com/ --format html

# Convert to Markdown
python web_to_doc.py --url https://docs.example.com/ --format md

# Convert to JSON
python web_to_doc.py --url https://docs.example.com/ --format json

# Convert to DOCX (Microsoft Word)
python web_to_doc.py --url https://docs.example.com/ --format docx
```

### Limiting Crawl Depth

```bash
# Only crawl 2 levels deep
python web_to_doc.py --url https://docs.example.com/ --max-depth 2
```

### Content Filtering

```bash
# Only include pages containing specific keywords
python web_to_doc.py --url https://docs.example.com/ --contains "guide,tutorial,reference"

# Exclude pages containing specific keywords
python web_to_doc.py --url https://docs.example.com/ --not-contains "deprecated,obsolete"
```

### Using Sitemaps

```bash
python web_to_doc.py --url https://docs.example.com/ --use-sitemap
```

### Interactive Mode

```bash
python web_to_doc.py --url https://docs.example.com/ --interactive
```

This will first discover all URLs and then let you select which ones to include in the output.

### Generating a Table of Contents

```bash
python web_to_doc.py --url https://docs.example.com/ --toc
```

### Setting Request Delay

To be respectful to servers and avoid rate limiting:

```bash
# Wait 2 seconds between requests
python web_to_doc.py --url https://docs.example.com/ --delay 2
```

### Increasing Maximum Pages

```bash
# Process up to 500 pages
python web_to_doc.py --url https://docs.example.com/ --max-pages 500
```

## 📝 Command Line Arguments

| Argument | Description | Default |
|----------|-------------|---------|
| `--url` | URL to start crawling from | (Required) |
| `--output` | Output file path | `output.[format]` |
| `--format` | Output format: pdf, html, md, json, docx | `pdf` |
| `--max-depth` | Maximum depth to crawl | No limit |
| `--max-pages` | Maximum number of pages to process | 250 |
| `--delay` | Delay between requests in seconds | 1 |
| `--timeout` | Request timeout in seconds | 10 |
| `--contains` | Only include pages containing keywords (comma-separated) | None |
| `--not-contains` | Exclude pages containing keywords (comma-separated) | None |
| `--categories` | Only include pages from specified categories (comma-separated) | None |
| `--use-sitemap` | Use sitemap for URL discovery | False |
| `--sitemap-url` | URL of the sitemap | Auto-detect |
| `--toc` | Generate table of contents | False |
| `--interactive` | Interactive mode for URL selection | False |

## 🔍 How It Works

1. The tool starts crawling from the provided URL.
2. It extracts links from each page and follows them if they belong to the same domain and documentation area.
3. For each page, it extracts the main content, removing navigation, headers, footers, etc.
4. It processes the content for the selected output format, handling text, headings, code blocks, and images.
5. Finally, it generates the output file in the chosen format.

## 📄 Output Format Details

### PDF

- Creates a well-formatted PDF with proper styling for headings, paragraphs, and code blocks
- Images are included and properly sized
- Optional table of contents with page numbers

### HTML

- Single HTML file with embedded CSS
- All pages are included in one file
- Links to original sources are preserved
- Optional table of contents with anchor links

### Markdown

- Clean, readable Markdown format
- Headings, paragraphs, and links are preserved
- Optional table of contents with anchor links
- Suitable for GitHub wikis or other Markdown viewers

### JSON

- Structured JSON with URLs, titles, and text content
- Useful for further processing or data analysis

### DOCX (Microsoft Word)

- Microsoft Word document with proper formatting
- Images included
- Optional table of contents (needs to be updated in Word)

## 🛠️ Technical Details

Web-to-Doc is built using:

- **requests**: For HTTP requests and downloading content
- **BeautifulSoup4**: For HTML parsing and content extraction
- **reportlab**: For PDF generation
- **Pillow**: For image processing
- **python-docx**: For DOCX creation (optional)
- **lxml**: For better XML handling (optional)

## 🤔 Common Issues & Solutions

### SSL Certificate Verification Failed

If you encounter SSL certificate issues, you may need to update your certificates or use the `--timeout` option with a higher value.

### Content Not Being Extracted Properly

Different websites have different structures. If the content isn't being extracted correctly, try looking at the generated HTML output to see what content is being captured.

### Images Not Loading

Some websites block image downloads based on referer headers. The tool includes a user-agent header but some sites may still block the requests.

### Rate Limiting

If you're being rate-limited, increase the `--delay` parameter to add more time between requests.

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Special thanks to all contributors
- Created with assistance from Claude AI (Anthropic)

---

*If you find this tool helpful, consider starring the repository or contributing to its development!*