# Social Media Homepage with Vue.js

This project is a simple social media homepage designed using Vue.js. The page displays posts retrieved from a mock API along with their associated comments. Users' avatars are fetched from [Picsum.photos](https://picsum.photos/) to add a visual aspect to each post.

## Features
- **Display Posts**: Posts are fetched from the mock API endpoint `https://jsonplaceholder.typicode.com/posts`.
- **Load Comments**: Comments are fetched from `https://jsonplaceholder.typicode.com/comments?postId=<postId>`. Comments are shown on demand with a "Load More Comments" button.
- **Infinite Scroll**: As users scroll to the bottom of the page, more posts are automatically loaded.
- **User Avatars**: Random user avatars are generated using [Picsum.photos](https://picsum.photos/).
- **User Names**: Each post is associated with a user, and their name is displayed next to their post. The names are mapped to user IDs.

![Vue 3 Social media homepage Project](public/video.gif)

### Installation and Setup

1. Clone the repository to your local machine:

    ```bash
    git clone https://github.com/rajkumar-ravichandiran/vue-social-media.git
    ```

2. Navigate to the project directory:

    ```bash
    cd vue-social-media
    ```

3. Install the dependencies:

    ```sh
   npm install
   ```

4. Compile and Hot-Reload for Development:

    ```sh
   npm run dev
   ```

4. Compile and Minify for Production:

    ```sh
   npm run build
   ```