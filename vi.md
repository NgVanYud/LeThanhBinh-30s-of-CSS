# 30 giây cho CSS  
Bộ sưu tập những đoạn CSS hữu ích mà bạn có thể hiểu trong 30 giây hoặc ngắn hơn  
## Bouncing loader  
`HTML`  
```
    <div class="bouncing-loader">
      <div></div>
      <div></div>
      <div></div>
    </div>
```  
`CSS`  
```
    @keyframes bouncing-loader {
      from {
        opacity: 1;
        transform: translateY(0);
      }
      to {
        opacity: 0.1;
        transform: translateY(-1rem);
      }
    }
    .bouncing-loader {
      display: flex;
      justify-content: center;
    }
    .bouncing-loader > div {
      width: 1rem;
      height: 1rem;
      margin: 3rem 0.2rem;
      background: #8385aa;
      border-radius: 50%;
      animation: bouncing-loader 0.6s infinite alternate;
    }
    .bouncing-loader > div:nth-child(2) {
      animation-delay: 0.2s;
    }
    .bouncing-loader > div:nth-child(3) {
      animation-delay: 0.4s;
    }
```  
**Giải thích:**  
*Ghi chú:* `1rem` thường là `16px`  
1. `@keyframes` định nghĩa một animation có 2 trạng thái, nơi mà phần thử thay đổi `opacity` và đã được tịnh tiến trên nên 2D sử dụng `transform: translateY()`  
2. `.bouncing-loader` là vùng chưa cha của bouncing circles và sử dụng `display : flex` và `justify-content: center` để đặt chúng vào giữa  
3.  `.bouncing-loader > div` chỉ đến 3 `div` con của cha để đặt mẫu. Những thẻ `div` được đặt cho chiều rộng và chiều cao `1rem`, sử dụng `border-radius: 50%` để thay đổi chúng từ ô vuông sang vòng tròn.  
4. `margin: 3rem 0.2rem` quy định mỗi vòng tròn có lề trên/dưới `3rem` và trái/phải `0.2rem` sao cho không trỏ trực tiếp vào từng phần thử khác nhau, giving them some breathing room.  
5. `animation` là một đặc tính được sử dụng để viết tắt cho nhiều đặc tính animation: `animation-name`, `animation-duration`, `animation-iteration-count`, `animation-direction`  
6. `nth-child(n)` trỏ đến thành phần là con thứ n của cha nó.  
7. `animation-delay` được sử dụng cho `div`  tương ứng thứ hai và ba, sao cho mỗi phần tử không bắt đầu cùng lúc.  

**Hỗ trợ trình duyệt**  
95.3%    
Không có thông báo trước  
* https://caniuse.com/#feat=css-animation  

## tùy chỉnh box-sizing  
tùy chỉnh box-model sao cho `chiều rông` và `chiều dài` không bị ảnh hưởng bởi `boder` và `padding`  
`CSS`  
```
    html {
      box-sizing: border-box;
    }
    *,
    *::before,
    *::after {
      box-sizing: inherit;
    }
```  
**Giải thích**  
1. `box-sizing: border-box` làm cho các thuộc tính thêm vào của `padding` hoặc `border` không ảnh hướng đến ` chiều rộng ` và ` chiều cao ` của thành phần.  
2. `box-sizing: inherit` làm cho thành phần có liên quan đến quy định về `box-sizing` của cha nó.  

**Hỗ trợ trình duyệt**  
98.4%    
Không có thông báo trước  
* https://caniuse.com/#feat=css3-boxsizing  

## Circle  
Tạo vòng tròn với CSS thuần  
`HTML`  
```
    <div class="circle"></div>
```   
`CSS`  
```
    .circle {
      border-radius: 50%;
      width: 2rem;
      height: 2rem;
      background: #333;
    }
```  
**Giải thích**  
`border-radius: 50%` làm cong viền của thành phần để tạo vòng tròn  
Đường tròn có bán kính là như nhau tại tất cả mọi điểm, nên ` chiều rộng ` và ` chiều cao` là như nhau. Với giá trị khác sẽ thành hình elip  
 
**Hỗ trợ trình duyệt**  
95.5%    
Không có thông báo trước  
* https://caniuse.com/#feat=border-radius  

## Clearfix  
Đảm bảo rằng các thành phần tử tự dọn dẹp các con của nó  
###### Ghi chú: Nó chỉ hữu ích nếu bạn vẫn sử dụng float để xây dựng các layout. Hãy cân nhắc sử dụng các cách tiếp cận hiện đai với bố cục flexbox hay grid  
`HTML`  
```
    <div class="clearfix">
      <div class="floated">float a</div>
      <div class="floated">float b</div>
      <div class="floated">float c</div>
    </div>
```  
`CSS`  
```
    .clearfix::after {
      content: '';
      display: block;
      clear: both;
    }
    .floated {
      float: left;
    }
```    

**Giải thích**  
1. `.clearfix::after` : Định nghĩa một thành phần giả định  
2. `content: ''` cho phép thành phần giả định ảnh hưởng tới bố cục  
3. `clear ; both` Chỉ ra rằng bên trái, bên phải hay cả hai bên của thành phần không thể liền kề với các phần thử float trước đó bên trong cùng một khối bối cảnh  

**Hỗ trợ trình duyêt**  
99+%  
* Để cho đoạn trích này làm việc đúng, bạn cần đảm bảo rằng không có phần tử con không float nào trong vùng chứa và không có phần float cao nào đứng trước vùng clearfix nhưng trong cùng một định dạng bối cảnh  

## Không thay đổi tỷ lệ của chiều rộng với chiều cao  
Gán chiều rộng không đổi cho thành phần, nó sẽ đảm bảo chiều cao của nó vẫn còn tương xứng trong chế độ responsive (tỷ lệ chiều rộng và chiều cao của nó vẫn tương xứng nhau)  
`HTML`  
```
    <div class="constant-width-to-height-ratio"></div>
```  
`CSS`  
```
    .constant-width-to-height-ratio {
      background: #333;
      width: 50%;
    }
    .constant-width-to-height-ratio::before {
      content: '';
      padding-top: 100%;
      float: left;
    }
    .constant-width-to-height-ratio::after {
      content: '';
      display: block;
      clear: both;
    }
```  
**Demo**  
Thay đổi kích cỡ cửa sổ trình duyệt của bạn để thấy tỉ lệ của của thành phần vẫn như cũ  
**Giải thích**  
`padding-top` ở trên phần tử giả định `::before` là nguyên nhân chiều cao của thành phần có tỷ lệ ngang với chiều rộng của nó. Chính vì `100%` mà chiều cao của thành phần sẽ luôn chiếm `100%` chiều rộng, tạo hình vuông responsive  
Phương pháp này cũng cho phép nội dung được đặt bên trong thành phần bình thường.  
## Counter  
Counter về bản chất là các biến được duy trì bởi CSS mà giá trị có thể tăng lên bởi các quy định của CSS để theo dõi xem nó được sử dụng bao nhiêu lần  
`HTML`  
```
    <ul>
      <li>List item</li>
      <li>List item</li>
      <li>List item</li>
    </ul>
```  
`CSS`  
```
    ul {
      counter-reset: counter;
    }
    li::before {
      counter-increment: counter;
      content: counters(counter, '.') ' ';
    }
```  
**Giải thích**  
Bạn có thể tạo một danh sách sắp xếp sử dụng bất cứ mẫu nào của HTML  
1. `counter-reset` Khởi tạo counter, giá trị là tên của counter. Theo mặc định, counter bắt đầu từ 0. Đặc tính này cũng có thể được sử dụng để thay đổi giá trị của nó với bất cứ số riêng nào  
2. `counter-incremenet` Sử dụng phần tử có thể đếm được. Mỗi `counter-reset` được khởi tạo, giá trị của counter có thể tăng hoặc giảm  
3. `counter(name, style)` Hiển thị giá trị của phần counter. Phần lớn được sử dụng trong đặc tính `content`. Hàm này có thể nhận 2 tham số, thứ nhất là tên của counter, cái thứ hai có thể là `decimal` hoặc `upper-roman` (mặc định là `decimal`)  
4. `counters(counter, string, style)` Hiển thị giá trị của phần counter. Phần lớn được sử dụng trong ~~đặc tính~~(property - **thuộc tính**) `content`. Hàm này có thể nhận 3 tham số, thứ nhất là tên của counter, cái thứ hai có thể bao gồm một chuỗi mà ở đằng sau counter, cái thứ ba có thể là `decimal` hoặc `upper-roman` (mặc định là `decimal`)  
5. CSS counter có thể đặc biệt hữu ích để tạo danh sách phác thảo, bởi vì ví dụ mới của counter là tự động sinh ra trong thành phần con. Sử dụng hàm `counters()`, tách văn bản có thể chèn vào giữa các tầng khác nhau của các counter lồng nhau.  

**Hỗ trợ trình duyêt**  
98.4%  
* https://caniuse.com/#feat=css-counters  
## Tùy chỉnh thanh cuộn  
Việc tùy chỉnh lại mẫu của thanh cuộn cho tài liệu và phần tử scrollable overflow, trên nền tảng Webkit  
`HTML`  
```
    <div class="custom-scrollbar">
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure id exercitationem nulla qui repellat laborum vitae, molestias tempora velit natus. Quas, assumenda nisi. Quisquam enim qui iure, consequatur velit sit?</p>
    </div>
```  
`CSS`  
```
    /* Document scrollbar */
    ::-webkit-scrollbar {
      width: 8px;
    }
    ::-webkit-scrollbar-track {
      box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
      border-radius: 10px;
    }
    ::-webkit-scrollbar-thumb {
      border-radius: 10px;
      box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.5);
    }
    /* Scrollable element */
    .some-element::webkit-scrollbar {
    }
```  
**Giải thích**  
1. `::-webkit-scrollbar` trỏ tới toàn bộ thành phần thanh cuộn  
2. `::-webkit-scrollbar-track` chỉ chọn thành phần thanh cuộn đang theo dõi  
3. `::-webkit-scrollbar-thumb` trỏ vào thanh cuộn thumb  

**Hỗ trợ trình duyêt**  
88.0%  
* https://caniuse.com/#feat=css-scrollbar  

## Tùy chỉnh bộ chọn văn bản  
Thay đổi mẫu của bộ chọn văn bản  
`HTML` 
```
    <p class="custom-text-selection">Select some of this text.</p>
    CSS
``` 
`CSS`  
```
    ::selection {
      background: aquamarine;
      color: black;
    }
    .custom-text-selection::selection {
      background: deeppink;
      color: white;
    } 
```  
**Giải thích**  
`::selection` định nghĩa bộ chọn giả định trên thành phần để tạo mẫu văn bản bên trong nó khi mà đã được chọn. Lưu ý rằng nếu bạn không phối hợp với bất cứ bộ chọn nào khác, mẫu của bạn sẽ áp dụng với tài liệu mức gốc với bất kì thành phần nào được chọn.  
  
**Hỗ trợ trình duyêt**  
84.9%  
* Yêu cầu tiền tố để hỗ trợ đầy đủ và không thực sự đúng trong bất kỳ hoàn cảnh nào.*  
* https://caniuse.com/#feat=css-selection  

## Tùy chỉnh biến  
Các biến CSS mà chứa các giá trị riêng có thể sử dụng lại trong suốt tài liệu  
`HTML`  
```
    <p class="custom-variables">CSS is awesome!</p>
```  
`CSS`  
```
    :root {
      --some-color: #da7800;
      --some-keyword: italic;
      --some-size: 1.25em;
      --some-complex-value: 1px 1px 2px whitesmoke, 0 0 1em slategray, 0 0 0.2em slategray;
    }
    .custom-variables {
      color: var(--some-color);
      font-size: var(--some-size);
      font-style: var(--some-keyword);
      text-shadow: var(--some-complex-value);
    }
```  
**Giải thích**  
Các biến được định nghĩa toàn cục bên trong lớp giả định CSS  `:root` mà ứng với phần tử gốc của cây đại diên tài liệu. Các biến cũng có thể khoanh vùng thành một bộ chọn nếu định nghĩa bên trong khối.  
Khai báo biến với `--variable-name:`.  
Tái sử dụng biến khắp tài liệu sử dụng `var(--variable-name)`.  

**Hỗ trợ trình duyêt**  
88.0%  
* https://caniuse.com/#feat=css-variables  

## Vô hiệu hóa bộ chọn  
Tạo một nội dung không thể chọn  
`HTML`  
```
    <p>You can select me.</p>
    <p class="unselectable">You can't select me!</p>
```  
`CSS`  
```
    .unselectable {
      user-select: none;
    }
```  
**Giải thích**  
`user-select: none` quy định rằng văn bản không thể được lựa chọn  
**Hỗ trợ trình duyêt**  
87.2%  
*Yêu cầu tiền tố để hỗ trợ toàn bộ. Nó không phải là luồng đảm bảo để ngăn chặn người dùng sao chép nội dung*  
* https://caniuse.com/#feat=css-variables  

## Donut spinner  
Tạo một Donut spinner sử dụng để biểu thị rằng đang load nội dung  
`HTML`  
```
    <div class="donut"></div>
```  
`CSS`  
```
    @keyframes donut-spin {
      0% {
        transform: rotate(0deg);
      }
      100% {
        transform: rotate(360deg);
      }
    }
    .donut {
      display: inline-block;
      border: 4px solid rgba(0, 0, 0, 0.1);
      border-left-color: #7983ff;
      border-radius: 50%;
      width: 30px;
      height: 30px;
      animation: donut-spin 1.2s linear infinite;
    }
```  
**Giải thích**  
Sử dụng semi-transparent `border` cho toàn bộ thành phần, ngoại trừ những thứ mà đóng vai trò như loading chỉ thị cho donut. sử dụng `animation` để quay thành phần  
 **Hỗ trợ trình duyêt**  
 95.3%  
 * Yêu cầu tiền tố để hỗ trợ toàn bộ.
 * https://caniuse.com/#feat=css-animation  
 *  https://caniuse.com/#feat=transforms2d  

## Bóng động  
Tạo các bóng giống như `box-shadow` nhưng dựa trên màu cơ bản của chính các thành phần  
`HTML`  
```
    <div class="dynamic-shadow-parent">
      <div class="dynamic-shadow"></div>
    </div>
```  
`CSS`  
```
    .dynamic-shadow-parent {
      position: relative;
      z-index: 1;
    }
    .dynamic-shadow {
      position: relative;
      width: 10rem;
      height: 10rem;
      background: linear-gradient(75deg, #6d78ff, #00ffb8);
    }
    .dynamic-shadow::after {
      content: '';
      width: 100%;
      height: 100%;
      position: absolute;
      background: inherit;
      top: 0.5rem;
      filter: blur(0.4rem);
      opacity: 0.7;
      z-index: -1;
    }
```  
**Giải thích**  
*The snippet requires a somewhat complex case of stacking contexts to get right, such that the pseudo-element will be positioned underneath the element itself while still being visible*.  
1. `position: relative` ở phần tử cha thiết lập định nghĩa vị trí Cartesian cho các phần tử con.    
2. `z-index:1` thiếp lập 1 lớp định nghĩa mới  
3. `: relative` ở phần tử con thiết lập dịnh nghĩa vị trí cho phần tử giả định  
4. `::after` định nghĩa 1 phần tử giả định  
4. `position: absolute` tách phần tử giả định ra khỏi luồng tài liệu và đặt nó ở vị trí relation với cha nó.  
6. `width: 100% and height: 100%` làm kích thước phần tử giả định lấp đầy kích thước cha nó, làm nó cần bằng về kích thước.  
7. `background: inherit` khiến phần tử giả định thừa kế quy định về góc tuyến tính trên phần tử.  
8. `top: 0.5rem` làm nhô phần tử giả định xuống dưới cha nó.  
9. `filter: blur(0.4rem)` sẽ làm mờ phần từ mẫu để tạo bóng phía dưới.  
10. `opacity: 0.7` khiến phần tử giả định trong suốt 1 phần  
11. `z-index: -1` đặt phần tử giả định sau cha của nó  

**Hỗ trợ trình duyêt**  
91.7%  
*Yêu cầu tiền tố để hỗ trợ toàn bộ  
* https://caniuse.com/#feat=css-filters  

## Tối giảm các biến  
Các biến có thể sử dụng lại cho thuộc tính `transition-timing-function`, mạnh mẽ hơn là sử dụng `ease`, `ease-in`, `ease-out` và `ease-in-out`  
`HTML`  
```
    <div class="easing-variables"></div>
```   
`CSS`  
```
    :root {
      --ease-in-quad: cubic-bezier(0.55, 0.085, 0.68, 0.53);
      --ease-in-cubic: cubic-bezier(0.55, 0.055, 0.675, 0.19);
      --ease-in-quart: cubic-bezier(0.895, 0.03, 0.685, 0.22);
      --ease-in-quint: cubic-bezier(0.755, 0.05, 0.855, 0.06);
      --ease-in-expo: cubic-bezier(0.95, 0.05, 0.795, 0.035);
      --ease-in-circ: cubic-bezier(0.6, 0.04, 0.98, 0.335);
      --ease-out-quad: cubic-bezier(0.25, 0.46, 0.45, 0.94);
      --ease-out-cubic: cubic-bezier(0.215, 0.61, 0.355, 1);
      --ease-out-quart: cubic-bezier(0.165, 0.84, 0.44, 1);
      --ease-out-quint: cubic-bezier(0.23, 1, 0.32, 1);
      --ease-out-expo: cubic-bezier(0.19, 1, 0.22, 1);
      --ease-out-circ: cubic-bezier(0.075, 0.82, 0.165, 1);
      --ease-in-out-quad: cubic-bezier(0.455, 0.03, 0.515, 0.955);
      --ease-in-out-cubic: cubic-bezier(0.645, 0.045, 0.355, 1);
      --ease-in-out-quart: cubic-bezier(0.77, 0, 0.175, 1);
      --ease-in-out-quint: cubic-bezier(0.86, 0, 0.07, 1);
      --ease-in-out-expo: cubic-bezier(1, 0, 0, 1);
      --ease-in-out-circ: cubic-bezier(0.785, 0.135, 0.15, 0.86);
      }
      .easing-variables {
        width: 50px;
        height: 50px;
        background: #333;
        transition: transform 1s var(--ease-out-quart);
      }
      .easing-variables:hover {
        transform: rotate(45deg);
      }
```  
**Giải thích**  
Các biến được định nghĩa toàn cục bên trong lớp giả định CSS :root mà ứng với phần tử gốc của cây đại diên tài liệu. Trong HTML, `:root` đại diện cho thành phần `<html>` và tương đương bộ chọn `html`, ngoại trừ đặc tính của nó là cao hơn  
**Hỗ trợ trình duyệt**  
88.0%  
*Không cảnh báo*  
* https://caniuse.com/#feat=css-variables  

## Văn bản khắc  
Tạo hiệu ứng tại chỗ văn bản xuất hiện để "khắc" hoặc khắc vào nền  
`HTML`  
```
    <p class="etched-text">I appear etched into the background.</p>
```  
`CSS`  
```
    .etched-text {
      text-shadow: 0 2px white;
      font-size: 1.5rem;
      font-weight: bold;
      color: #b8bec5;
    }
```  
**Giải thích**  
`text-shadow: 0 2px white` tạo bóng trắng cách `0px` theo chiều ngang và `2px` theo chiều dọc từ vị trí xuất phát.  
Nền cần phải tối hơn bóng để hiệu ứng có thể làm việc  
Màu của chữ phải nhạt đi để làm cho khi nhìn như là được khắc lên nền  
**Hỗ trợ trình duyệt**  
98.1%  
*Không cảnh báo*  
* https://caniuse.com/#feat=css-textshadow  

## Phân phối đều các thành phần con  
Phân phối đều các thành phần con bên trong thành phần cha  
`HTML`  
```
    <div class="evenly-distributed-children">
      <p>Item1</p>
      <p>Item2</p>
      <p>Item3</p>
    </div>
```  
`CSS`  
```
    .evenly-distributed-children {
      display: flex;
      justify-content: space-between;
    }
```  
**Giải thích**  
1. `display : flex` cho phép flex-box  
2. `justify-content: space-between` phân phối đều các thành phần con theo chiều ngang. Mục đầu tiên sẽ được đặt vào cạnh trái, trong khi mục cuối được đặt vào góc phải.  
Cách khác, sử dụng `justify-content: space-around` để phân phối các thành phần con với không gian xung quanh chúng, chứ không phải là giữa chúng.  

**Hỗ trợ trình duyệt**  
98.1%  
*Cần tiền tố để hỗ trợ đầy đủ*  
* https://caniuse.com/#feat=flexbox  

## Flexbox centering  
định vị giữa thành phần theo chiều ngang và chiều dọc bên trong thành phần cha sử dụng `flexbox`  
`HTML`  
```
    div class="flexbox-centering">
      <div class="child">Centered content.</div>
    </div>
```  
`CSS`  
```
    CSS
    .flexbox-centering {
      display: flex;
      justify-content: center;
      align-items: center;
    }
```  
**Giải thích**  
1. `display: flex` cho phép flexbox.  
2. `justify-content: center` căn giữa thành phần con theo chiều ngang.  
3. `align-items: center` căn giữa thành phần con theo chiều dọc  

**Hỗ trợ trình duyệt**  
98.1%  
*Cần tiền tố để hỗ trợ đầy đủ*  
* https://caniuse.com/#feat=flexbox  

## Văn bản dốc  
Cho văn bản màu đổ dốc  
`HTML`  
```
    <p class="gradient-text">Gradient text</p>
```  
`CSS`  
```
    .gradient-text {
      background: -webkit-linear-gradient(pink, red);
      -webkit-text-fill-color: transparent;
      -webkit-background-clip: text;
    }
```  
**Giải thích**  
1. `background: -webkit-linear-gradient(...)` đưa cho thành phần văn bản nền dốc.  
2. `webkit-text-fill-color: transparent` điền văn bản với màu trong suốt.  
3. `webkit-background-clip: text` clips nền với văn bản, điền văn bản với nền dốc như là màu sắc  

**Hỗ trợ trình duyêt**  
91.5%  
*Sử dụng các thuộc tính không chuẩn  
* https://caniuse.com/#feat=text-stroke  

## căn giữa lưới  
căn giữa thành phần con theo chiều ngang và chiều dọc bên trong thành phần cha sử dụng `grid`  
`HTML`  
```
    <div class="grid-centering">
      <div class="child">Centered content.</div>
    </div>
```  
`CSS`  
```
    .grid-centering {
      display: grid;
      justify-content: center;
      align-items: center;
    }
```  
**Giải thích**  
1. `display: flex` cho phép grid.  
2. `justify-content: center` căn giữa thành phần con theo chiều ngang.  
3. `align-items: center` căn giữa thành phần con theo chiều dọc  

**Hỗ trợ trình duyêt**  
87.6%  
*Không cảnh báo*  
* https://caniuse.com/#feat=css-grid  

## Grid layout  
Bố cục trang web cơ bản sử dụng `grid`  
`HTML`  
```
    <div class="grid-layout">
      <div class="header">Header</div>
      <div class="sidebar">Sidebar</div>
      <div class="content">
        Content
        <br>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit.
      </div>
      <div class="footer">Footer</div>
    </div>
```  
`CSS`  
```
    .grid-layout {
      display: grid;
      grid-gap: 10px;
      grid-template-columns: repeat(3, 1fr);
      grid-template-areas:
        'sidebar header header'
        'sidebar content content'
        'sidebar footer  footer';
      color: white;
    }
    .grid-layout > div {
      background: #333;
      padding: 10px;
    }
    .sidebar {
      grid-area: sidebar;
    }
    .content {
      grid-area: content;
    }
    .header {
      grid-area: header;
    }
    .footer {
      grid-area: footer;
    }
```  
**Giải thích**  
1. `display: grid` cho phép grid.  
2. `grid-gap: 10px` định nghĩa khoảng các giữa các thành phần  
3. `grid-template-columns: repeat(3, 1fr)` định nghĩa 3 cột với kích thước như nhau  
4. `grid-template-areas` định nghĩa tên của khu vực lưới  
5. `grid-area: sidebar` tạo thành phần sử dụng khu vực lưới có tên `sidebar`  

**Hỗ trợ trình duyệt**  
87.6%  
*Không cảnh báo*  
* https://caniuse.com/#feat=css-grid  

## Hairline border  
Gán cho thành phần viền tương ứng 1 điểm ảnh tự nhiên của thiết bị theo chiều ngang mà nhìn rất nhọn và sắc nét  
`HTML`  
```
    <div class="hairline-border">text</div>
```  
`CSS`  
```
    .hairline-border {
      box-shadow: 0 0 0 1px;
    }
    @media (min-resolution: 2dppx) {
      .hairline-border {
        box-shadow: 0 0 0 0.5px;
      }
    }
    @media (min-resolution: 3dppx) {
      .hairline-border {
        box-shadow: 0 0 0 0.33333333px;
      }
    }
    @media (min-resolution: 4dppx) {
      .hairline-border {
        box-shadow: 0 0 0 0.25px;
      }
    }
```  
**Giải thích**  
1. `box-shadow` chỉ khi sử dụng rộng rãi, thêm vào viền giả định mà có thể sử dụng điểm ảnh phụ  
2. sử dụng `@media (min-resolution: ...)` để kiểm tra tỉ lệ điểm ảnh của thiết bị (`1dppx` tương đương 96 DPI), cài đặt sự lan tràn của `shadow-box` tương đương `1 / dppx`  

**Hỗ trợ trình duyệt**  
95.5%  
*Cần các cú pháp luân phiên và JavaScript, người dùng chủ động kiểm tra để hỗ trợ đầy đủ    
* https://caniuse.com/#feat=css-boxshadow  
* https://caniuse.com/#feat=css-media-resolution  

*Chrome không hỗ trợ gia trị subpixel trên `border`. Safari không hỗ trợ gia trị subpixel trên `box-shadow`. Firefox hỗ trợ subpixel trên tất cả  

## Hoạt ảnh hover gạch chân  
Tạo hiệu ứng hoạt ảnh gạch chân khi văn bản được hover vào  
##### **credit:** https://flatuicolors.com/ #####  
`HTML`  
```
    <p class="hover-underline-animation">Hover this text to see the effect!</p>
```  
`CSS`  
```
    .hover-underline-animation {
      display: inline-block;
      position: relative;
      color: #0087ca;
    }
    .hover-underline-animation::after {
      content: '';
      position: absolute;
      width: 100%;
      transform: scaleX(0);
      height: 2px;
      bottom: 0;
      left: 0;
      background-color: #0087ca;
      transform-origin: bottom right;
      transition: transform 0.25s ease-out;
    }
    .hover-underline-animation:hover::after {
      transform: scaleX(1);
      transform-origin: bottom left;
    }
```  
**Giải thích**  
1. `display: inline-block` khiến khối p và inline-block tránh kẻ chân từ việc kéo dài chiều dài cha nó hơn nội dung(chữ)  
2. `position: relative` trên phần tử thiết lập định nghĩa vị trí Cartesian cho phần tử giả định  
3. `::after` định nghĩa phần tử giả định  
4. `position: absolute` mang phần tử giả định ra khỏi luồng tài liệu và đặt nó relation với cha nó  
5. `width: 100%` đảm bảo phần tử giả định trải dài toàn bộ chiều rộng của khối chữ  
6. `transform: scaleX(0)` khởi tạo scale cho phần từ giả định về 0 để nó không có chiều rộng và không hiện  
7. `bottom: 0 và left: 0` đặt nó ở góc dưới trái của khối  
8. `transition: transform 0.25s ease-out` thay đổi transform sẽ được chuyển trong 0.25 giấy với hàm tính giờ ease-out. 
9. `transform-origin: bottom right` thay đổi điểm neo là đặt tại góc dưới bên phải khối  
10. `:hover::after` sau đó dùng scaleX(1) để chuyển đổi chiều rộng thành 100%, sau đó thay đổi transform-origin thành bottom left để điểm neo ngược lại, cho phép nó chuyển đổi sang hướng khác khi hover ra  

*Hỗ trợ trình duyệt**  
*Không có cảnh báo*  
* https://caniuse.com/#feat=transforms2d  
* https://caniuse.com/#feat=css-transitions  

## Theo dõi dốc theo con trỏ chuột  
Hiệu ứng hover chỗ dốc theo con trỏ chuột  

`HTML`  
```
    <button class="mouse-cursor-gradient-tracking">
      <span>Hover me</span>
    </button>
```  
`CSS`  
```
    .mouse-cursor-gradient-tracking {
      position: relative;
      background: #7983ff;
      padding: 0.5rem 1rem;
      font-size: 1.2rem;
      border: none;
      color: white;
      cursor: pointer;
      outline: none;
      overflow: hidden;
    }
    .mouse-cursor-gradient-tracking span {
      position: relative;
    }
    .mouse-cursor-gradient-tracking::before {
      --size: 0;
      content: '';
      position: absolute;
      left: var(--x);
      top: var(--y);
      width: var(--size);
      height: var(--size);
      background: radial-gradient(circle closest-side, pink, transparent);
      transform: translate(-50%, -50%);
      transition: width 0.2s ease, height 0.2s ease;
    }
    .mouse-cursor-gradient-tracking:hover::before {
      --size: 200px;
    }
```  
`Javascript`  
```
    var btn = document.querySelector('.mouse-cursor-gradient-tracking')
    btn.onmousemove = function(e) {
      var x = e.pageX - btn.offsetLeft
      var y = e.pageY - btn.offsetTop
      btn.style.setProperty('--x', x + 'px')
      btn.style.setProperty('--y', y + 'px')
    }
```  
**Giải thích**  
*TODO*  
**Ghi chú!**  
Nếu trường hợp cha của thành phần được định vị (`position: relative`), bạn sẽ cần phải bỏ đi phần bù của nó như sau:  
```
    var x = e.pageX - btn.offsetLeft - btn.offsetParent.offsetLeft
    var y = e.pageY - btn.offsetTop - btn.offsetParent.offsetTop
```  
**Hỗ trợ trình duyêt**  
88.0%  
*yêu cầu Javascript*  
* https://caniuse.com/#feat=css-variables  

## Bộ chọn :not  
Bộ chọn giả định `:not` hữu ích cho định dạng kiểu cho nhóm thành phần, khi mà bỏ lại thành phần cuối (hoặc chỉ định) không tạo kiêu  
`HTML`  
```
    <ul class="css-not-selector-shortcut">
      <li>One</li>
      <li>Two</li>
      <li>Three</li>
      <li>Four</li>
      <li>Five</li>
    </ul>
```  
`CSS`  
```
    .css-not-selector-shortcut {
      display: flex;
    }
    li {
      list-style-type: none;
      margin: 0;
      padding: 0 0.75rem;
    }
    li:not(:last-child) {
      border-right: 2px solid #d2d5e4;
    }
```  
**Giải thích**  
`li:not(:last-child)` quy định rằng kiểu được áp dụng cho tất cả các thành phần `li` ngoại trừ `:last-child`  
**Hỗ trợ trình duyệt**  
98.4%  
*Không có cảnh báo*  
* https://caniuse.com/#feat=css-sel3  

## Overflow scroll gradient  
Thêm hiệu ứng dốc mờ dần cho các thành phần tràn để hiển thị tốt hơn nhiều nội dung cuộn lại  
`HTML`  
```
    <div class="overflow-scroll-gradient">
      <div class="overflow-scroll-gradient__scroller">
        Content to be scrolled
      </div>
    </div>
```   
`CSS`  
```
    .overflow-scroll-gradient {
      position: relative;
    }
    .overflow-scroll-gradient::after {
      content: '';
      position: absolute;
      bottom: 0;
      width: 240px;
      height: 25px;
      background: linear-gradient(
        rgba(255, 255, 255, 0.001),
        white
      ); /* transparent keyword is broken in Safari */
      pointer-events: none;
    }
    .overflow-scroll-gradient__scroller {
      overflow-y: scroll;
      background: white;
      width: 240px;
      height: 200px;
      padding: 15px 0;
      line-height: 1.2;
      text-align: center;
    }
```  
**Giải thích**  
1. `position: relative` trên phần tử cha thiết lập 1 định nghĩa vị trí Cartesian cho phần tử giả định.
2. `::after` định nghĩa 1 phần tử giả định
3. `background-image: linear-gradient(...)` thêm 1 dốc tuyến tính mờ dần từ trong suốt trên trắng (trên xuống dưới)
4. `position: absolute` đấy phần tử giả định ra khỏi luồng tài liệu và đặt vị trí nó relation với cha nó.
5. `width: 240px` gán kích thước của phần tử cuộn ( con của cha có phần tử giả định)
6. `height: 25px` là chiều cao của phần tử giả định mờ dốc, nên giữ nhỏ tương đối
7. `bottom: 0` đặt vị trí phần tử giả định dưới cùng của ch
8. `pointer-events: none` quy định phần tử giả định không thể bị chọn với sự kiện chuột, cho phép chữ đắng sau vẫn có thể được chọn/ tương tác  

**Hỗ trợ trình duyệt**  
*Không có cảnh báo*  
* https://caniuse.com/#feat=css-gradients  

## Danh sách hiện ra  
Xuất hiện 1 menu tương tác bật ra khi hover.  
`HTML`  
```
    <div class="reference">
      <div class="popout-menu">
        Popout menu
      </div>
    </div>
```  
`CSS`  
```
    .reference {
      position: relative;
    }
    .popout-menu {
      position: absolute;
      visibility: hidden;
      left: 100%;
    }
    .reference:hover > .popout-menu {
      visibility: visible;
    }
```  
**Giải thích**  
1. `position: relative` ở phần tử cha liên quan thiết lập định nghĩa vị trí cho con nó
2. `position: absolute` mang menu bật ra khỏi luồng tài liệu và đặt nó relation với cha nó
3. `left: 100%` chuyển menu về phía trái 100% của cha nó
4. `visibility: hidden` khởi tạo ẩn menu và cho phép chuyển đổi (không giống display: none)
5. `.reference:hover > .popout-menu`   khi .reference được hover, chọn ngay lập tức con với class .popout-menu và thay đổi visibility của chúng thành visible, sẽ hiện cái menu bật ra.  

**Hỗ trợ trình duyệt**  
99+%  
*Không có cảnh báo*  

## Gạch chân văn bản đẹp  
1 thay thế đẹp hơn của text-decoration: underline khi phần hạ xuống không ghim gạch dưới. Thực hiện tự nhiên 1text-decoration-skip-ink: auto1 nhưng khó kiểm soát gạch dưới hơn  
`HTML`  
```
    <p class="pretty-text-underline">Pretty text underline without clipping descending letters.</p>
```  
`CSS`  
```
    .pretty-text-underline {
      font-family: Arial, sans-serif;
      display: inline;
      font-size: 18px;
      text-shadow: 1px 1px 0 #f5f6f9, -1px 1px 0 #f5f6f9, -1px -1px 0 #f5f6f9, 1px -1px 0 #f5f6f9;
      background-image: linear-gradient(90deg, currentColor 100%, transparent 100%);
      background-position: 0 0.98em;
      background-repeat: repeat-x;
      background-size: 1px 1px;
    }
    .pretty-text-underline::-moz-selection {
      background-color: rgba(0, 150, 255, 0.3);
      text-shadow: none;
    }
    .pretty-text-underline::selection {
      background-color: rgba(0, 150, 255, 0.3);
      text-shadow: none;
    }
```  
**Giải thích**  
1. `text-shadow: ...` có 4 giá trị với phần bù cover khu vực 4x4 pixel để đảm bảo phần gạch chân có bóng `dày` để cover đường chỗ ghi tên clip nó. Sử dụng màu mà hợp với nền. Với font lớn hơn, sử dụng kích cỡ `px` lớn hơn  
2. `background-image: linear-gradient(...)` tạo dốc 90 độ với với màu chữ hiện tại (`currentColor`)  
3. Thuộc tính `background-*` tạo độ lớn cho dốc tương đương 1x1 px ở dưới và lặp lại nó theo x-axis  
4. Bộ chọn giả định `::selector` đảm bảo rằng bóng của văn bản không gây trở ngại với bộ chọn văn bản  

**Hỗ trợ trình duyệt**  
95.4%  
Khoảng cách của phần gạch chân từ văn bản phụ thuộc vào chỉ số của font, vì vậy bạn cần phải chắc chắn rằng mọi người nhìn các font như nhau (chẳng hạn như những font không có hệ thống mà sẽ thay đổi dựa trên hệ điều hành)  
* https://caniuse.com/#feat=css-textshadow  
* https://caniuse.com/#feat=css-gradients      

## Đặt lại tất cả các kiểu  
Đặt lại tất cả các kiểu về mặc định với một thuộc tính. Nó sẽ không ảnh hưởng thuộc tính `direction ` và `unicode-bidi`  
`HTML`  
```
    <div class="reset-all-styles">
      <h4>Title</h4>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure id exercitationem nulla qui repellat laborum vitae, molestias tempora velit natus. Quas, assumenda nisi. Quisquam enim qui iure, consequatur velit sit?</p>
    </div>
```  
`CSS`  
```
    .reset-all-styles {
      all: initial;
    }
```  
**Giải thích**   
Thuộc tính `all` cho phép bạn đặt lại tất cả kiểu (kế thừa hoặc không) về giá trị mặc định.  
**Hỗ trợ trình duyệt**  
88.3%  
*Trạng thái MS Edge đang được xem xét*  
* https://caniuse.com/#feat=css-all  

## Shape separator  
Sử dụng dạng SVG để tách rời hai khối khác nhau để tạo cảm giác thú vị hơn so với tách biệt theo tiêu chuẩn ngang  
`HTML`  
```
    <div class="shape-separator"></div>
```  
`CSS`  
```
    .shape-separator {
      position: relative;
      height: 48px;
      background: #333;
    }
    .shape-separator::after {
      content: '';
      background-image: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIHN0cm9rZS1saW5lam9pbj0icm91bmQiIHN0cm9rZS1taXRlcmxpbWl0PSIxLjQxNCI+PHBhdGggZD0iTTEyIDEybDEyIDEySDBsMTItMTJ6IiBmaWxsPSIjZmZmIi8+PC9zdmc+);
      position: absolute;
      width: 100%;
      height: 24px;
      bottom: 0;
    }
```  
**Giải thích**  
1. `position: relative` trên mỗi phần tử thiết lập một vùng định vị Cartesian cho phần tử giả định  
2. `::after` định nghĩa phần tử giả định  
3. `background-image: url(...)` thêm khối SVG (1 tam giác 24x24 trên định dạng base64) như là ảnh nền của phần tử mẫu, mặc định tự lặp. Nó phải cùng màu với khối được chia  
4. `position: absolute` mang phần tử giải định ra khỏi tài liệu và đặt nó ở vị trí relation với cha nó
5. `width: 100%` đảm bảo phần tử trải dài chiều rộng cha nó
6. `height: 24px` là chiều cao tương tự như khối.
7. `bottom: 0` đặt phần tử giả định ở cuối cha nó  

**Hỗ trợ trình duyệt**  
98.3%  
*Không có cảnh báo*  
* https://caniuse.com/#feat=svg  

## Sibling fade  
Làm mờ đi như nhau các thành phần được hover    
`HTML`  
```
    <div class="sibling-fade">
      <span>Item 1</span>
      <span>Item 2</span>
      <span>Item 3</span>
      <span>Item 4</span>
      <span>Item 5</span>
      <span>Item 6</span>
    </div>
```  
`CSS`  
```
    span {
      padding: 0 1rem;
      transition: opacity 0.2s;
    }
    .sibling-fade:hover span:not(:hover) {
      opacity: 0.5;
    }
```  
**Giải thích**  
1. `transition: opacity 0.2s` quy định thay đổi độ mờ sẽ chuyển đổi trong 0.2 giây  
2. `.sibling-fade:hover span:not(:hover)` quy định rằng khi cha được hover, chọn bất cứ `span` con nào mà đang không được hover và thay đổi độ mờ của nó thành `0.5`   

**Hỗ trợ trình duyệt**  
95.4%  
*Không có cảnh báo*  
* https://caniuse.com/#feat=css-sel3  
* https://caniuse.com/#feat=css-transitions   

## Ngắn xếp font hệ thống  
Sử dụng các font tự nhiên của hệ điều hành để tạo cảm giác tự nhiên cho ứng dụng   
`HTML`  
```
    <p class="system-font-stack">This text uses the system font.</p>
```  
`CSS`  
```
    .system-font-stack {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu,
        Cantarell, 'Helvetica Neue', Helvetica, Arial, sans-serif;
    }
```  
**Giải thích**  
Trình duyệt tìm kiếm mỗi font kế tiếp, ưu tiên cái đầu tiên có thể, và đến tiếp cái tiếp theo nếu không thể tìm thấy font(trên hệ thống hoặc định nghĩa trong css)  
1. `-apple-system` là San Francisco, sử dụng trên iOs và macOs(tuy nhiên không phải Chrome)
2. `BlinkMacSystemFont` là San francisco, sử dụng trên macOs chrome
3. `Segoe UI` sử dụng trên Windows 10
4. `Roboto` sử dụng trên Android
5. `Oxygen-Sans` sử dụng trên GNU+Linux
6. `Ubuntu` sử dụng trên Linux
7. `"Helvetica Neue"` và `Helvetica` sử dụng trên macOS 10.10 và thấp hơn (gói trong trích dẫn vì nó có khoảng trống)
8. `Arial` là font được sử dụng rỗng rãi bởi tất cả hệ điều hành
9. `sans-serif` là font sans-serif dự phòng khi không cái nào khác hộ trợ  

**Hỗ trợ trình duyêt**  
99+%  
*Không có cảnh báo*  

## Tam giác  
Tạo hình tam giác với CSS thuần  
`HTML`  
```
    <div class="triangle"></div>
```  
`CSS`  
```
    .triangle {
      width: 0;
      height: 0;
      border-top: 20px solid #333;
      border-left: 20px solid transparent;
      border-right: 20px solid transparent;
    }
```  
**Giải thích**  
[Xem link này để có giải thích chi tiết](https://stackoverflow.com/questions/7073484/how-do-css-triangles-work)  
Màu của viền là màu của tam giác. Cạnh của tam giác tương ứng với thuộc tính `border-*`. Ví dụ, màu trên `border-top` nghĩa là điểm nhọn bên dưới  
Thử nghiệm với giá trị `px` để thay đổi tỉ lệ của tam giác  
**Hỗ trợ trình duyệt**  
99+%  
*Không có cảnh báo*  

## Ngắt bỏ văn bản  
Nếu văn bản dài hơn một dòng, nó sẽ ngắt bỏ với dấu ba chấm  
`HTML`  
```
    <p class="truncate-text">If I exceed one line's width, I will be truncated.</p>
```   
`CSS`  
```
    .truncate-text {
      overflow: hidden;
      white-space: nowrap;
      text-overflow: ellipsis;
      width: 200px;
    }
```  
**Giải thích**  
1. `overflow: hidden` ngăn ngừa văn bản bị tràn từ kích thước của nó (với một khối, chiều rộng 100% và chiều cao tự động).  
2. `white-space: nowrap` ngăn ngừa văn bản vượt quá một dòng theo chiều cao  
3. `text-overflow: ellipsis` làm nó kết thức bởi dấu ba chấm nếu văn bản vượt quá kích thước của nó  
4. `width: 200px` đảm bảo rằng phần tử có kích thước, để biết khi nào có dấu ba chấm  

**Hỗ trợ trình duyệt**  
98.4%  
*Chỉ hoạt động với những thành phần một dòng*  
* https://caniuse.com/#feat=text-overflow