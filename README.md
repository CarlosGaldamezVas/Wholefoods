# Output Examples
* [JSON](/OUTPUT.json)
* [CSV](/OUTPUT.csv)


| Title                                | Price     | Link                                                        |
|--------------------------------------|-----------|-------------------------------------------------------------|
| Boneless Beef Ribeye Steak           | $17.99/lb | /product/meat-boneless-beef-ribeye-steak-b07qzcksy2         |
| Boneless Beef New York Strip Steak   | $17.99/lb | /product/meat-boneless-beef-new-york-strip-steak-b079vxcby1 |
| Beef Tenderloin Steak (Filet Mignon) | $31.99/lb | /product/meat-beef-tenderloin-steak-filet-mignon-b07811nqgn |
| Ground Beef 80% Lean/ 20% Fat        | $5.99/lb  | /product/meat-ground-beef-80-lean-20-fat-b07yfsxpsy         |
| Boneless Beef Chuck Roast            | $7.99/lb  | /product/meat-boneless-beef-chuck-roast-b07815gm3n          |
| Bone In Beef Ribeye Steak            | $16.99/lb | /product/meat-bone-in-beef-ribeye-steak-b07815wps3          |


# Usage
Example URL: https://www.wholefoodsmarket.com/products/meat/beef

- Press `Command+Option+i` on your Mac or `F12` on your PC to open Inspect Element on your browser
- Open the console:\
  - ![](https://github.com/DWWF/Wholefoods/blob/910e615441463c140b42ccffb88f22a6f7a36b99/console_example.png)
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
# Convert the JSON Output to CSV
* Use https://data.page, or any other JSON to CSV conversion tool.
