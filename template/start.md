# Getting Started - Craft Documentation

- [Gist](https://gist.github.com/extratone/05ad6f35ca1c4a4e4b2710f2c9ea5389)
- [Craft Publish](https://www.craft.do/s/9cy9qPoZ69cJBn)

---

<script src="https://gist.github.com/extratone/05ad6f35ca1c4a4e4b2710f2c9ea5389.js"></script>

---

Craft extensions are packaged as ZIP files (named with a `.craftx` file type) that contain various internal files. In the following example, we are going showcase one of the simplest extensions which can be created - it consists of only three files:

#### manifest.json

```json
{
  "id": "do.craft.hello",
  "name": "Hello World",
  "fileName": "hello-world",
  "author": "Craft Docs",
  "author-email": "team@craft.do",
  "description" : "Joyfully greets world citizens",
  "api": "0.1.0",
  "main": "index.html"
}
```


The [manifest file](https://documentation.developer.craft.do/extensions/manifest-file) is the entry point of the extension. It describes some essential metadata (e.g. plugin name, author) and describes where the main application code is located (e.g. `index.html`).

#### index.html

```html
<!DOCTYPE html>
<html>
  <body>
    <button id="btn-execute">Greet</button>
    <script>
      const button = document.getElementById("btn-execute")

      button.addEventListener("click", async () => {
        const block = craft.blockFactory.textBlock({ 
          content: "Hello world!"
        })

        await craft.dataApi.addBlocks([ block ])
      })
    </script>
  </body>
</html>
```


This is where the application code is located. In this example, the code places a single button in the extension UI. When that button is pressed, the code uses the `craft` global object for accessing the [Craft API](https://documentation.developer.craft.do/extensions/craft-api). In this case, it is used for creating a new block with some placeholder text and adding it to the current document.

This is a very simple extension with only a few lines of code. Real-world extensions can consist of thousands of lines of complex application code and even for those, all the code needs to be bundled into a single HTML file. This can be achieved in various ways, but we recommend using our [project templates](https://documentation.developer.craft.do/extensions/tools/project-templates) for bundling your application code.

Every extension **must** have a unique icon that helps to distinguish it from other extensions. To help you get started quickly, we made you a [default extension icon](https://res.craft.do/assets/default-craft-extension-icon.png) to use while your extension is in development.

### icon.png

`curl https://res.craft.do/assets/default-craft-extension-icon.png --output icon.png`

## Packaging

The three files above must be packaged into a single ZIP file that has the `.craftx` filename extension.

`zip -vr hello-world.craftx icon.png index.html manifest.json`

## Running the extension

### Web editor

Once the extension package is ready, we can install it into the Craft editor. First, you need to make sure that extensions are enabled: goto the space dropdown in the top left corner and click on **Craft eXtensions**.

![](https://827995558-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FbDnZb2Co0NsBLcTp1L0A%2Fuploads%2FuLlnTtj9el47tfNQgjTQ%2Fenable-extensions.png?alt=media&token=dbfba4fb-18cc-4fac-b6be-10ab49588a90)

Make sure that extensions are enabled.

After that you can install the package from the extension section of the sidebar. Extensions are only available from within a document view.

![Extension sidebar when no extensions are installed](https://827995558-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FbDnZb2Co0NsBLcTp1L0A%2Fuploads%2FUv8FlNgmhXM8AjzZN2UX%2Fhello-1.png?alt=media&token=d27950b8-f6b4-419d-b2e4-6b3c1d1ea2f4)

After the extension is installed you will see it appear in the extension list.

![Hello World extension is in place](https://827995558-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FbDnZb2Co0NsBLcTp1L0A%2Fuploads%2FvOAhJBtqgXCQ1hJaLnXH%2Fhello-2.png?alt=media&token=5234bb61-1937-49e6-bc54-f7f843257d25)

Tap on the name of your extension to open the extension UI. If you are following this sample code you will see the single button we created in the code earlier. Click, or tap the button and you will see the placeholder text we defined earlier injected into the currently open document.

![After clicking our button a few times](https://827995558-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FbDnZb2Co0NsBLcTp1L0A%2Fuploads%2FoLtWaTGBZhrhbN4zjjdN%2Fhello-3.png?alt=media&token=eafd1c55-4998-4448-9131-5eb378f2137b)