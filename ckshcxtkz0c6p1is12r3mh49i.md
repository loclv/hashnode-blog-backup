## Tại sao cần dùng Fonts API? Cách dùng 🌲 Nuxt.js với nuxt-webfontloader

## Tại sao cần dùng Fonts API?

Nhiều trang web sử dụng font có sẵn trên OS - hệ điều hành hoặc hệ thống sẽ gặp phải vấn đề font sẽ rất xấu nếu không được cài sẵn các loại font dễ nhìn.
Ngoài ra, OS font sẽ sai khác về độ dài và độ cao của chữ, gây khó khăn cho designer và developer giữ đúng tỷ lệ design.

Giải pháp là dùng API để get về font đẹp và xịn sò, luôn hiển thị đúng yêu cầu ở mọi môi trường.

Vấn đề về thời gian downloading font thì chỉ gặp phải ở lần đầu tiên tải font đó thôi, từ lần sai browser sẽ cache lại nên không phải download về nữa.
Điều này giúp tận dụng được font resource giữa các trang web với nhau.
Ví dụ trang web A đã load font `Roboto` rồi thì nếu web B cũng cần font `Roboto`, khi ta truy cập web B thì ta không cần phải download về nữa.
Điều này tham khảo tại [developers.google.com/fonts/faq](https://developers.google.com/fonts/faq):

>The font files themselves are cached for one year, which cumulatively has the effect of making the entire web faster: When millions of websites all link to the same fonts, they are cached after visiting the first website and appear instantly on all other subsequently visited sites.

Thông thường để tiết kiệm chi phí ta hay dùng các font miễn phí, mà cá nhân mình thấy hay được sử dụng nhất là font được cung cấp bởi API của Google -
[fonts.google.com](https://fonts.google.com/).
Google họ chỉ host miễn phí resource là font thôi, còn người thiết kế những font đó thông thường là họ chia sẻ miễn phí qua `github`.

## Sử dụng `nuxt-webfontloader` trong `Nuxt.js`

[nuxt-webfontloader](https://github.com/Developmint/nuxt-webfontloader) là 1 wrapper của
[Google's/Typekit's webfontloader](https://github.com/typekit/webfontloader) dành riêng cho [Nuxt.js](https://nuxtjs.org/).
Tại sao dùng [webfontloader](https://github.com/typekit/webfontloader) thì hẹn ở bài viết khác nhé.


Thêm vào package.json - dependencies:

```sh
yarn add nuxt-webfontloader
```

Chẳng hạn ta dùng font `Lato`.
Thêm mudule vào `nuxt.config.js`:

```js
export default {
  modules: ['nuxt-webfontloader'],
  webfontloader: {
    google: {
      families: ['Lato:400,700'], // Loads Lato font with weights 400 and 700
    },
  },
}
```

Giờ ta set `font-family` cho `body` của web: `font-family: Lato;`.
Tuy nhiên do luật [stylelint - font-family-no-missing-generic-family-keyword](https://stylelint.io/user-guide/rules/list/font-family-no-missing-generic-family-keyword/),
nên ta phải thêm 1 font-family thông thường.
Font-family thông thường hay generic font là font có sẵn trên hệ thống hay OS.
Ví dụ `sans-serif` là font thông thường:

`pages/index.vue`:

```vue
<style>
body {
  font-family: Lato, sans-serif;
}
</style>
```

Luật này nhằm mục đích giải quyết vấn đề tại thời điểm mà browser chưa caching và đang load font chính lên để hiển thị.
Font thay thế để hiển thị text sẽ là font thông thường được set phía sau font chính kia. Khoảng thời gian này người ta gọi là
[FOUT - Flash Of Unstyled Text](https://en.wikipedia.org/wiki/Flash_of_unstyled_content).
Thường thì khoảng thời gian này chỉ diễn ra nửa giây và chỉ xảy ra vào lần đầu load web thôi.
Để tái hiện `FOUR` nhiều lần thì ta bật develop tool của Chrome - `Ctrl` + `shift` + `P`, rồi vào tab `netwwork` và reload lại web -  `Ctrl` + `R`.

Ảnh chụp text khi chưa load xong font chính - font hiển thị là `sans-serif`:

![chưa load xong font chính.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629282764509/AB8worUR3.png)

Ảnh chụp text khi load xong font chính - font hiển thị là `Lato`:

![load xong font chính.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629282739599/P2m1GA4Vd.png)

Bạn có thấy font khác nhau không?

![thinking](https://media.giphy.com/media/3oz8xZvvOZRmKay4xy/giphy.gif)

[Bài viết How to Fix FOUT (Flash of Unstyled Text) in React](https://dev.to/fyfirman/how-to-fix-fout-flash-of-unstyled-text-in-react-1dl1) sẽ giải quyết vấn đề này.
Có thể sau này mình sẽ viết 1 bài tiếng Việt về cách làm sao fix FOUT trong Vue.

Cuối cùng xóa bỏ `stylesheets` cũ không cần thiết nếu có ở `template` hoặc `nuxt.config.js`.
Nếu là `nuxt.config.js` phần `head` thì xóa bỏ:

```js
export default {
  head:{
    link: [
      // You don't need that line anymore!
      { rel: 'stylesheet', href: 'https://fonts.googleapis.com/css?family=Lato:400,700' }
    ]
  }
}
```

## Tham khảo

- [nuxt-webfontloader](https://github.com/Developmint/nuxt-webfontloader)
- [Google's/Typekit's webfontloader](https://github.com/typekit/webfontloader)
- [stylelint - font-family-no-missing-generic-family-keyword](https://stylelint.io/user-guide/rules/list/font-family-no-missing-generic-family-keyword/)

---

Photo by <a href="https://unsplash.com/@quanquan1115?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Yusong He</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
