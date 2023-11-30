# Reveal.js for Blueinno Lesson Slides

This project uses [reveal.js](https://revealjs.com/) and its [markdown plugin](https://revealjs.com/markdown/) to create lesson slides.

The purpose of this project is to:

1. Easier translation from rundown to slides.
2. Easier to keep track of changes with git.
3. Easier to create various versions of slides.
4. Easier and better visualization of code changes for students.
5. Adds functionalities that are not available in Google Slides. (e.g. auto syntax highlighting, auto code changes animation, iframe embedding, etc.)

For now:

- This project only contains an example of 402D L01 slides.
- This project is not meant to be hosted online for security reasons.
- UI options of selecting from multiple lesson markdown files are not planned yet.

## Usage

### 1. Install

1. Clone this repository

    ```bash
    git clone https://github.com/felix-blueinno/reveal.js-lesson-slides.git
    ```

2. Install dependencies

      ```bash
      npm install
      ```

3. Run the server

      ```bash
      npm start
      ```

4. Open <http://localhost:8000> to view the slides.

### 2. Edit

1. In `index.html`, find the following line:

    ```html
    <div class="reveal">
      <div class="slides">
        <section 
          data-markdown="./markdowns/402D_L01_Slides.md" 
          data-separator="---" 
          data-separator-vertical="____"
          data-separator-notes="^Note:" 
          data-charset="utf-8">
        </section>

      </div>
    </div>
    ```

2. Base on lines above, you can see that the markdown file is `./markdowns/402D_L01_Slides.md`. You can change it to any markdown file you want.

3. Use triple "-" (dash) to separate slides, and use triple "_" (underscore) to separate vertical slides.