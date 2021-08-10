## Thử 🏃‍♀️ chạy chart.js trên web đơn giản


## 👋 Giới thiệu

[Chart.js](https://www.chartjs.org/) là thư viện dành cho `JavaScript` thuần để vẽ các loại đồ thị phổ biến.

Bên cạnh các Chart lib dành cho riêng các Framework/lib như `React`, `Angular`, `Vue`, `Svelte`..., thì `chart.js` có thể dùng được ở mọi nơi mà không cần Framework nào cả.

Cũng chính điều này là điểm yếu của `chart.js` khi không tận dụng được sức mạnh của các Framework/lib hiện đại.

Ngoài ra [source-code của Chart.js](https://github.com/chartjs/Chart.js) không được viết bằng `TypeScript`.

Web trong bài viết này sẽ chạy thử đoạn [source-code giới thiệu](https://www.chartjs.org/docs/latest/#creating-a-chart) của `chart.js`.

## 🎒 Chuẩn bị

Cài đặt NodeJs có thể dùng [nvm](https://github.com/nvm-sh/nvm) - Node Version Manager.

Cài [pnpm](https://pnpm.io/) - NodeJs package manager tiết kiệm dung lượng ổ cứng, tương tự như `yarn`, `npm`:

```sh
npm install -g pnpm
```

Khởi tạo `package.json`:

```sh
pnpm init -y
cat package.json
```

Ta thấy file `package.json` trống không. Ta tiếp tục cài [npm - chart.js](https://www.npmjs.com/package/chart.js):

```sh
pnpm i chart.js
```

Output:

```txt
Packages are hard linked from the content-addressable store to the virtual store.
  Content-addressable store is at: /home/{your-username}/.pnpm-store/v3
  Virtual store is at:             node_modules/.pnpm
Progress: resolved 1, reused 0, downloaded 1, added 1, done

dependencies:
+ chart.js 3.5.0
```

Trong file `package.json` đã có:

```json
"dependencies": {
  "chart.js": "^3.5.0"
}
```

Phiên bản `chart.js` ta đang dùng ở đây là `3.5.0`.

Khởi tạo `index.html`:

```sh
touch index.html
code index.html
```

## 💅 Vẽ 1 chart đơn giản

Copy đoạn code dưới đây vào `index.html`:

```html
<!DOCTYPE html>
<html>
  <style>
    .wrapper {
      width: 400px;
      height: 400px;
    }
  </style>
  <body>
    <h1>My First Chart.js web!</h1>

    <div class="wrapper">
      <canvas id="myChart" width="400" height="400"></canvas>
    </div>

    <script src="node_modules/chart.js/dist/chart.js"></script>

    <script>
      const ctx = document.getElementById('myChart').getContext('2d');
      const myChart = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
          datasets: [
            {
              label: '# of Votes',
              data: [12, 19, 3, 5, 2, 3],
              backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)',
              ],
              borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)',
              ],
              borderWidth: 1,
            },
          ],
        },
        options: {
          scales: {
            y: {
              beginAtZero: true,
            },
          },
        },
      });
    </script>
  </body>
</html>

```

Mở trực tiếp file `html` này bằng browser như `Chrome`, ta thấy biểu đồ đã được vẽ:

![Screenshot from 2021-08-10 15-38-16.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628586816720/Zi--jX-MK.png)

## 🕵️‍♀️ Giải thích source-code

Ta để ý tham số đầu tiên sẽ là `ctx` - [CanvasRenderingContext2D](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D) lấy từ DOM element của thẻ `canvas` thông qua `id="myChart"`.

`CanvasRenderingContext2D` là 1 phần của bộ `Canvas API`, cung cấp nội dung 2D được render (vẽ) ra trên bề mặt thẻ `canvas`.

Thử tưởng tượng thằng này nó cũng giống như 1 khung tranh mà ta có thể vẽ và xóa đi bất cứ cái gì mà ta muốn.

`type: 'bar'` mô tả loại đồ thị là các cột thẳng đứng có độ cao thấp phụ thuộc vào số liệu.

`labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange']` là tên của các loại data, được ghi bên dưới cột.

`label: '# of Votes'` là phần chú thich trên cùng.

`backgroundColor`, `borderColor`, `borderWidth` là style của từng cột theo thứ tự array.

Phần `options.scales.y`, `beginAtZero: true` tức là các cột sẽ được vẽ từ mốc data từ `0`.

Nếu set là `false` thì các cột sẽ được vẽ từ mốc data của cột thấp nhất, và cũng vì thế nên cột thấp nhất có độ cao là `0`.

Như vậy là ta đã dùng thử xong ví dự cơ bản của `chart.js`.

## 📖 Tham khảo

- [w3schools.com/html](https://www.w3schools.com/html/tryit.asp?filename=tryhtml_script)

---

Photo by <a href="https://unsplash.com/@bash__profile?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Nicholas Cappello</a> on <a href="https://unsplash.com/s/photos/chart?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
