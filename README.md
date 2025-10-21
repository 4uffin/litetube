>[!WARNING]
>
> To avoid major frustration from Google and the YouTube Team, this project requires **You** to supply your own API key for access to YouTube related data and information.

# **LiteTube: A Lightweight Tube Viewing Experience**

> A lightweight Tube viewing experience.

LiteTube is a client-side, single-page web application I designed for a streamlined, minimalist experience when searching and viewing YouTube content. Built primarily with **HTML, CSS, and modern Vanilla JavaScript**, this project demonstrates strong client-side development principles, efficient API interaction, and performance optimization techniques.

It's an excellent example of a **LocalStorage-based web app** that utilizes the YouTube Data API for search and the YouTube Iframe Player API for robust video playback management.

## **📜 License**

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE).

## **🚀 Features**

I built LiteTube with a focus on efficiency, persistence, and a clean user experience.

* **API Key Persistence:** Your YouTube Data API key is securely stored in **LocalStorage** and pre-filled on subsequent visits if the "Remember Key" option is checked. The key is masked for security after initial entry.

* **Persistent Search State:** The last successful search query, current search filters, and the nextPageToken are saved to **LocalStorage** to maintain the application's state across sessions.

* **Fully Responsive Layout:** The application adapts fluidly. On desktops ($\>1024$px), it uses a 50/50 split for results and the player. On mobile and smaller screens, it automatically switches to a stacked, column layout.

* **Advanced Search Filters:** Filter results by **Sort Order** (Relevance, Date, View Count), **Duration** (Short, Medium, Long), and **Upload Date** (Last Hour, Day, Week, Month, Year).

* **Efficient Data Fetching:** I use asynchronous JavaScript (async/await) and Promise.all() to simultaneously fetch detailed video statistics (views, duration) and channel statistics (subscriber count) after the initial search.

* **Custom Player Error Handling:** I implement the YouTube Iframe Player API to detect and handle playback errors (e.g., embedding disabled by the creator). A custom error overlay displays an "Open on YouTube" fallback button when an error is detected.

* **Load More Pagination:** I implement continuous loading for results using the API's nextPageToken for a seamless "infinite scroll" experience.

* **Optimized Rendering:** I employ a **DocumentFragment** to batch multiple DOM insertions when displaying search results, minimizing layout thrashing and improving rendering performance.

## **💻 Technology Stack**

| Language/Tool | Purpose |
| :---- | :---- |
| **HTML5** | Core structure and semantic markup. |
| **CSS3** | Minimal in-line styling and a single \<style\> block for layout and responsiveness. |
| **JavaScript (ES6+)** | All application logic, API interaction, state management, and DOM manipulation. |
| **YouTube Data API v3** | Searching for videos and fetching statistics/details. |
| **YouTube Iframe Player API** | Handling video playback and detecting embed errors. |
| **LocalStorage** | Persistence for API key and last application state. |

## **🛠️ Setup and Usage**

### **1. Obtain a YouTube Data API Key**

To use LiteTube, you must have a valid YouTube Data API v3 key:

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).  
2. Create a new project (if necessary).  
3. Enable the **YouTube Data API v3** service for your project.  
4. Create an **API key** under the **Credentials** section.

### **2. Run the Application**

This is a single HTML file application:

1. Save the project code as ```litetube.html```.  
2. Open ```litetube.html``` directly in any modern web browser.

### **3. Configure Your API Key**

1. Enter your **YouTube Data API key** into the input field at the top of the page.  
2. (Optional) Check the **"Remember Key"** box to save the key to your browser's LocalStorage.  
3. The main warning banner will disappear once a valid key is recognized.

### **4. Search and View**

1. Enter a search query (e.g., "latest technology breakthroughs") into the search input.  
2. Adjust filters (Sort, Duration, Date) as needed.  
3. Click **"Search Videos"** or press **Enter**.  
4. Click on any video in the results list to load it into the **Video Player**.

## **💡 Code Methodology Highlights**

### **1. Efficient Parallel Fetching**

To prevent a waterfall effect and speed up the display of rich result data (like views, subscribers, and duration), detail fetching is executed concurrently:
```
// Fetch details for all videos and their channels in parallel  
const [videoDetailsMap, channelDetailsMap] = await Promise.all([  
    fetchVideoDetails(videoIds, currentKey), // Gets views, duration, tags  
    fetchChannelDetails(channelIds, currentKey) // Gets subscriber count  
]);
```

### **2. Custom Player Error Handling**

The ```VideoPlayerController``` class intercepts API errors, providing a graceful fallback for users when the video creator has restricted embedding:
```
// Part of the VideoPlayerController class  
onPlayerError(event) {  
    // Error codes 150, 101, 153 typically indicate embedding is disabled.  
    if (event.data === 150 || event.data === 101 || event.data === 153) {  
        // Show an overlay with an external link instead of a broken player  
        this.showErrorOverlay(this.currentVideoId, "This video cannot be embedded. Please watch it on YouTube.");  
    }  
}
```

### **3. State Persistence with LocalStorage**

The core state is initialized and saved on every successful search, ensuring the user returns to the same search context:
```
// Initialization on load  
const savedKey = localStorage.getItem('youtubeApiKey');  
// ... other state loading ...

// Saving state after a successful search  
const saveState = () => {  
    localStorage.setItem('lastQuery', searchInput.value);  
    localStorage.setItem('sortOrder', sortSelect.value);  
    // ... other state saving ...  
    if (rememberKeyToggle.checked) {  
        localStorage.setItem('youtubeApiKey', apiKeyInput.value);  
    } else {  
        localStorage.removeItem('youtubeApiKey');  
    }  
};
```
