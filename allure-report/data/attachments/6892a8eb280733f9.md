# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: Session6\resizeWindow-Screenshot-File Upload.spec.ts >> Multiple file upload
- Location: tests\Session6\resizeWindow-Screenshot-File Upload.spec.ts:62:5

# Error details

```
Test timeout of 30000ms exceeded.
```

```
Error: page.goto: Test timeout of 30000ms exceeded.
Call log:
  - navigating to "https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_fileupload_multiple", waiting until "load"

```

# Page snapshot

```yaml
- generic [active]:
  - generic [ref=e2]:
    - link "" [ref=e3] [cursor=pointer]:
      - /url: https://www.w3schools.com
    - link "" [ref=e4] [cursor=pointer]:
      - /url: javascript:void(0);
    - link "" [ref=e5] [cursor=pointer]:
      - /url: javascript:void(0);
    - link "" [ref=e6] [cursor=pointer]:
      - /url: javascript:void(0);
    - link "" [ref=e7] [cursor=pointer]:
      - /url: javascript:void(0);
    - button "Run ❯" [ref=e8] [cursor=pointer]
    - link "Get your own website" [ref=e9] [cursor=pointer]:
      - /url: https://www.w3schools.com/spaces/
  - link [ref=e11]:
    - /url: javascript:void(0)
  - generic [ref=e12]:
    - text:   
    - generic [ref=e16]:
      - textbox [ref=e17]
      - generic [ref=e23]:
        - generic [ref=e25]: <!DOCTYPE html>
        - generic [ref=e27]: <html>
        - generic [ref=e29]: <body>
        - generic [ref=e33]: <form action="/action_page.php">
        - generic [ref=e35]: "Select files: <input type=\"file\" id=\"myFile\" name=\"img\" multiple>"
        - generic [ref=e37]: <input type="submit">
        - generic [ref=e39]: </form>
        - generic [ref=e43]: <p>Click the "Try it" button to find out if the file upload button accept multiple values (files).</p>
        - generic [ref=e47]: <button onclick="myFunction()">Try it</button>
        - generic [ref=e51]: <p id="demo"></p>
        - generic [ref=e55]: <script>
        - generic [ref=e57]: "function myFunction() {"
        - generic [ref=e59]: var x = document.getElementById("myFile").multiple;
        - generic [ref=e61]: document.getElementById("demo").innerHTML = x;
        - generic [ref=e63]: "}"
        - generic [ref=e65]: </script>
        - generic [ref=e69]: </body>
        - generic [ref=e71]: </html>
    - iframe [ref=e78]:
      - generic [active] [ref=f1e1]:
        - generic [ref=f1e2]:
          - text: "Select files:"
          - button "Choose File" [ref=f1e3]
          - button "Submit" [ref=f1e4]
        - paragraph [ref=f1e5]: Click the "Try it" button to find out if the file upload button accept multiple values (files).
        - button "Try it" [ref=f1e6]
        - paragraph
  - iframe [ref=e82]:
    - generic [active] [ref=f15e1]:
      - generic:
        - generic [ref=f15e3]:
          - img [ref=f15e5]
          - generic "Python - Comments - W3Schools.com" [ref=f15e6]
        - generic [ref=f15e11]:
          - generic [ref=f15e14]: "-01:22"
          - link [ref=f15e21] [cursor=pointer]:
            - /url: https://www.viously.com
  - img [ref=e86] [cursor=pointer]
```

# Test source

```ts
  1  | import test from "playwright/test";
  2  | 
  3  | test("resize window", async ({page})=>
  4  | {
  5  |   await page.goto("https://jqueryui.com/resources/demos/resizable/default.html");
  6  |   let resizeHandle=await page.locator('//div[@class="ui-resizable-handle ui-resizable-se ui-icon ui-icon-gripsmall-diagonal-se"]');
  7  | 
  8  |   let box=await resizeHandle.boundingBox();
  9  |   if(!box) throw new Error("Box not found");
  10 | 
  11 |   let x= box.x + 300;
  12 |   let y= box.y + 400;
  13 | 
  14 |   await resizeHandle.hover();
  15 |   await page.mouse.down();
  16 |   await page.mouse.move(x,y);
  17 |   await page.mouse.upp();
  18 | 
  19 | });
  20 | 
  21 | 
  22 | test("Screenshot without time-stamp", async ({page})=>
  23 | {
  24 |   await page.goto("https://playwright.dev/");
  25 | 
  26 |   //screenshot visible to eye
  27 |   await page.screenshot({ path: "Screenshot/VisibleToEye.png", fullPage:false });
  28 | 
  29 |   //screenshot of complete page including scroll
  30 | await page.screenshot({ path: "Screenshot/FullPage.png", fullPage:true });
  31 | 
  32 |   //screenshot of particulor webelement
  33 |   await page.locator('//h1[@class="hero__title heroTitle_ohkl"]').screenshot({ path: "Screenshot/Webelement.png"});
  34 | });
  35 | 
  36 | test("Screenshot with time-stamp", async ({page})=>
  37 | {
  38 |   await page.goto("https://playwright.dev/");
  39 | 
  40 |   const time=new Date().toISOString().replace(/[:;.]/g,"_");
  41 | 
  42 |   //screenshot visible to eye
  43 |   await page.screenshot({ path: `Screenshot/VisibleToEye_${time}.png`, fullPage:false });
  44 | 
  45 |   //screenshot of complete page including scroll
  46 | await page.screenshot({ path: `Screenshot/FullPage_${time}.png`, fullPage:true });
  47 | 
  48 |   //screenshot of particulor webelement
  49 |   await page.locator('//h1[@class="hero__title heroTitle_ohkl"]').screenshot({ path: `Screenshot/Webelement_${time}.png`});
  50 | });
  51 | 
  52 | test("Single file upload", async ({page})=>
  53 | {
  54 |   await page.goto("https://way2automation.com/way2auto_jquery/registration.php#load_box");
  55 | 
  56 |   //upload single file
  57 |   await page.locator("//input[@type='file']").setInputFiles("c:/Users/JASWANT/Desktop/Gmail - Resignation_- Jawahar Innani.pdf");
  58 |   
  59 | });
  60 | 
  61 | 
  62 | test("Multiple file upload", async ({page})=>
  63 | {
> 64 |   await page.goto("https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_fileupload_multiple");
     |              ^ Error: page.goto: Test timeout of 30000ms exceeded.
  65 | 
  66 |   //the webelement is inside iframe
  67 |   await page.frameLocator("//iframe[@id='iframeResult']").locator("//input[@id='myFile']").setInputFiles(["c:/Users/JASWANT/Desktop/Gmail - Resignation_- Jawahar Innani.pdf","c:/Users/JASWANT/Desktop/Electricity Bill.pdf"]);
  68 |   
  69 | });
```