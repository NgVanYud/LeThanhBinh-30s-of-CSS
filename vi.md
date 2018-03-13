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
4. `counters(counter, string, style)` Hiển thị giá trị của phần counter. Phần lớn được sử dụng trong đặc tính `content`. Hàm này có thể nhận 3 tham số, thứ nhất là tên của counter, cái thứ hai có thể bao gồm một chuỗi mà ở đằng sau counter, cái thứ ba có thể là `decimal` hoặc `upper-roman` (mặc định là `decimal`)  
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
The snippet requires a somewhat complex case of stacking contexts to get right, such that the pseudo-element will be positioned underneath the element itself while still being visible.  
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

