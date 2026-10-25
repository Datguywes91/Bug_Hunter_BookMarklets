# Bug_Hunter_BookMarklets
A curated arsenal of passive, client-side JavaScript bookmarklets for web application security testing. Designed for methodical, low-and-slow manual recon on VDPs and bug bounty targets, this toolkit bypasses the need for heavy proxies by executing directly within the browser's local environment. Features include DOM unmasking, modern SPA state harvesting, native XHR/Fetch hooking, and OAuth parameter manipulation. Safe, passive, and strictly scoped to local execution.


# Bug Bounty Bookmarklet Arsenal

A curated toolkit of 14 passive, client-side JavaScript bookmarklets designed for web application security testing and bug bounty reconnaissance. 

**Note on Usage:** All bookmarklets below are safe, passive, and strictly scoped to your local browser environment. They make no unauthorized outbound network requests. 

## How to Install
The easiest way to install the entire toolkit is to import the `bookmarks_import.html` file directly into your browser:
1. Download `bookmarks_import.html` from this repository.
2. Open your browser's Bookmark Manager (`Ctrl+Shift+O`).
3. Select the options/menu icon and click **Import Bookmarks**.
4. Select the downloaded HTML file. A new folder titled "Bug Bounty Arsenal" will appear on your bookmarks bar.

---

## PART 1: CORE RECONNAISSANCE & DOM MANIPULATION

### 1. The DOM Unmasker
- **Description:** Strips away visual barriers (hidden fields, disabled buttons, read-only tags) highlighting hidden attack surfaces directly on the page.
- **Use Case:** You land on a dashboard with greyed-out "Admin" buttons, hidden user-ID fields in a form, or password fields you want to view in plaintext.

### 2. The API/Endpoint Harvester
- **Description:** Scrapes the entire loaded HTML and inline scripts for relative paths and API endpoints, displaying them in a floating overlay.
- **Use Case:** You are testing a Single Page Application (SPA) and want to quickly map out API routes or find hidden administrative paths referenced in the frontend code.

### 3. The Client-State Dumper
- **Description:** Aggregates all client-side storage mechanisms (Cookies, Local Storage, Session Storage) into one readable view.
- **Use Case:** Quickly check for authorization tokens, role flags, or PII stored locally without having to manually dig through the browser's application tab.

### 4. The Native XHR & Fetch Spy
- **Description:** Monkey-patches the browser's native request functions to print all outbound payloads and inbound responses directly to the developer console.
- **Use Case:** Monitor asynchronous background requests and JSON responses natively without routing traffic through a proxy.

### 5. The Rapid OSINT Pivot
- **Description:** Extracts the current hostname and simultaneously opens three new tabs querying the Wayback Machine, crt.sh, and Shodan.
- **Use Case:** Discover an interesting subdomain and immediately map its history, find sibling subdomains, and check its open ports without interrupting your flow.

---

## PART 2: AUTHENTICATION & OAUTH

### 6. The OAuth Parameter Interrogator
- **Description:** Parses the current URL, isolates OAuth parameters, and specifically flags missing security controls like the state parameter.
- **Use Case:** Click "Sign in with Google" on your target, land on the provider's authorization page, and immediately highlight if you can tamper with the redirect_uri or if it lacks CSRF protection.

### 7. The Local JWT Harvester & Decoder
- **Description:** Scrapes your URL, LocalStorage, SessionStorage, and Cookies looking for a JWT signature. Base64-decodes the payload automatically.
- **Use Case:** Check if a newly issued session token is a JWT, where it is stored, and whether the payload contains manipulatable claims.

### 8. The Auth-Form Dissector
- **Description:** Strips away UI and dumps every form's destination and hidden parameters (like returnTo or redirect_url) into a text box.
- **Use Case:** Run on a login/registration page to isolate the backend endpoint and surface hidden routing parameters for Open Redirect or SSRF testing.

### 9. The SSO Link Extractor
- **Description:** Scans the DOM for any URLs pointing to common identity providers, unearthing buried legacy OAuth endpoints.
- **Use Case:** Quickly enumerate every third-party authentication integration a target supports to find alternate OAuth flows to test for ATO.

---

## PART 3: ADVANCED LOGIC & STATE

### 10. The SPA State Harvester
- **Description:** Extracts, formats, and dumps raw JSON application state used by modern frameworks like Next.js, Nuxt, and React.
- **Use Case:** Find PII, internal API keys, feature flags, and administrative endpoints leaked inside hidden JSON blobs embedded in the DOM.

### 11. The postMessage Interceptor
- **Description:** Monkey-patches outbound postMessage calls and hooks inbound message listeners, logging everything to the console.
- **Use Case:** Open a target page, interact with embedded widgets or OAuth popups, and watch the Developer Console to see what data is being passed cross-origin.

### 12. The Credential Autofill Honeypot
- **Description:** Injects an invisible form to test if browsers/password managers will blindly autofill stored credentials into injected HTML.
- **Use Case:** If you suspect an HTML injection or XSS vulnerability, run this to prove high-impact by instantly stealing plaintext credentials via autofill.

### 13. The Active OAuth Tamper-Matrix
- **Description:** Reads the current OAuth authorization URL and generates a matrix of one-click test URLs designed to break the flow.
- **Use Case:** Automatically test for CSRF, implicit flow downgrades, and Open Redirects on OAuth portals via an interactive clickable overlay.

### 14. The Local CSP & Header Auditor
- **Description:** Fetches the current page to extract security headers as they apply to an authenticated user and flags dangerous CSP directives.
- **Use Case:** Audit CORS and Content Security Policy dynamically after logging in to verify if restrictive policies actually apply to your session.
