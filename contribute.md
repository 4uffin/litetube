# **Contributing to LiteTube**

Thank you for considering contributing to LiteTube, a lightweight, client-side YouTube viewing experience I built with HTML, CSS, and Vanilla JavaScript. I welcome contributions from developers who appreciate clean code and efficient, single-file applications\!

## **💡 How to Contribute**

LiteTube's core philosophy is to remain a **single-file application** (litetube.html) that works entirely client-side, relying only on LocalStorage for persistence. All contributions must adhere to this structure.

### **1\. Suggesting Features or Reporting Bugs**

If you find a bug or have an idea for a new feature:

* **Bugs:** If you find something broken, please provide detailed steps on how to reproduce the issue (including your browser and operating system).  
* **Features:** LiteTube aims for minimalism. New features should enhance core functionality (search, playback, performance) without adding significant complexity or external dependencies.

### **2\. Making Code Changes**

When you are ready to make a change, please follow these steps:

1. **Fork the repository** (or copy the litetube.html file locally).  
2. **Make changes exclusively in litetube.html.** Do not create separate .js or .css files. All new JavaScript should be within the main \<script type="module"\> block.  
3. **Adhere to Code Style:**  
   * **JavaScript:** Use modern ES6+ syntax (const, let, arrow functions, async/await). Use JSDoc comments for any new functions or complex logic.  
   * **Styling:** Use in-line style attributes sparingly. Prefer adding new rules to the main \<style\> block in the \<head\> for global styles.  
   * **Responsiveness:** Always test and ensure your changes work seamlessly across mobile, tablet, and desktop views (referencing the existing applyLayout function).  
4. **Update Documentation (if necessary):** If your feature introduces a new dependency (e.g., another external script) or changes the core usage, update the README.md accordingly.  
5. **Submit the Code:** Once your changes are complete, submit them for review, clearly detailing what you changed and why.

## **🛠️ Development Practices**

Since LiteTube is built as a highly self-contained app, I value the following practices:

* **No External Frameworks:** I strictly avoid frameworks like React, Angular, Vue, or utility libraries like jQuery. Keep it Vanilla JavaScript.  
* **Performance First:** New features should not significantly harm the application's initial load time or search speed. Leverage performance tools like DocumentFragment when batching DOM updates (as seen in displayResults).  
* **API Key Safety:** Do not hardcode your YouTube API key. Always ensure the API key storage logic (using LocalStorage) is retained and functional.  
* **Error Handling:** If you interact with external APIs (like YouTube), include robust error handling (e.g., try...catch blocks) and graceful fallbacks for the user (like the current custom player error overlay).

I appreciate your effort and contribution to making LiteTube a better, faster experience\!