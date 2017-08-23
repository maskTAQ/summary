# (fixed并不是总是相对于窗口定位的)[https://codepen.io/huangbuyi/pen/mRYXbg]
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        container {
            width: 200px;
            height: 200px;
            line-height: 200px;
            text-align: center;
            background: #6699FF;
            animation: move 4s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }

        .fix {
            position: fixed;
            top: 20px;
            left: 20px;
            width: 200px;
            height: 200px;
            background: #9966FF;
            color: #FFF;
        }

        @keyframes move {
            0% {
                transform: translateX(100px);
            }
            50% {
                transform: translateX(500px);
            }
            100% {
                transform: translateX(100px);
            }
        }
    </style>
</head>

<body>
    <div class='container'>
        <div class='fix'>我固定了吗？</div>
    </div>
</body>

</html>
```