# Usage

- Press **Command+Option+i** on your Mac or **F12** on your PC to open Inspect Element on your browser

- Open the console:\
![](https://github.com/DWWF/Wholefoods/blob/7bffc54a740beb93d3432b9d74adf38824900dcb/Screenshot%202022-06-26%20050351.png)
- Copy and Paste the script into the console and hit enter
```javascript
const product_container = document.querySelectorAll(".w-pie--product-tile"); //Product Container
let data = [];

product_container.forEach((el) => {
  product_title = el.querySelector(
    '[data-testid="product-tile-name"]'
  ).textContent;
  product_price = el.querySelector(".regular_price").textContent;
  product_brand = el.querySelector(
    '[data-testid="product-tile-brand"]'
  ).textContent;
  wf_product_link = el
    .querySelector('[data-testid="product-tile-link"]')
    .getAttribute("href");
  data.push({
    Title: product_title,
    Brand: product_brand,
    Price: product_price,
    Link: wf_product_link,
  });
});

function downloadObjectAsJson(exportObj, exportName) {
  var dataStr =
    "data:text/json;charset=utf-8," +
    encodeURIComponent(JSON.stringify(exportObj));
  var downloadAnchorNode = document.createElement("a");
  downloadAnchorNode.setAttribute("href", dataStr);
  downloadAnchorNode.setAttribute("download", exportName + ".json");
  document.body.appendChild(downloadAnchorNode); // required for firefox
  downloadAnchorNode.click();
  downloadAnchorNode.remove();
}

downloadObjectAsJson(data, "OUTPUT");
```
