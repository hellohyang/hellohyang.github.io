<body>
    <canvas id="canvas" width="800" height="800"></canvas>
    <script>
        // 获取canvas画布绘制上下文对象以及获取2d画笔对象
        let canvas = document.getElementById("canvas");
        let ctx = canvas.getContext("2d");
 
        function render() {
            ctx.clearRect(0, 0, 800, 600);
 
            ctx.save() // 存档
            ctx.translate(400, 300) // 平移
            ctx.rotate(-Math.PI / 2) // 旋转
 
            ctx.save() // 存档
            for (let i = 0; i < 12; i++) {
                // 绘制小时的刻度
                ctx.beginPath()
                ctx.moveTo(170, 0)
                ctx.lineTo(190, 0)
                ctx.strokeStyle = 'gray';
                ctx.lineWidth = 8
                ctx.stroke()
                ctx.closePath()
                ctx.rotate(2 * Math.PI / 12)
            }
            ctx.restore() // 恢复上一层坐标
            ctx.save() // 存档
            for (let i = 0; i < 60; i++) {
                // 绘制分钟的刻度
                ctx.beginPath()
                ctx.moveTo(180, 0)
                ctx.lineTo(190, 0)
                ctx.strokeStyle = 'gray';
                ctx.lineWidth = 2
                ctx.stroke()
                ctx.closePath()
                ctx.rotate(2 * Math.PI / 60)
            }
            ctx.restore() // 恢复上一层坐标
            ctx.save() // 存档
 
            // 获取当前时间
            let time = new Date();
            let hour = time.getHours();
            let min = time.getMinutes();
            let sec = time.getSeconds();
            hour = hour >= 12 ? hour - 12 : hour; // 12小时制
            // 绘制时针
            ctx.rotate(2 * Math.PI / 12 * hour + 2 * Math.PI / 12 / 60 * min + 2 * Math.PI / 12 / 60 / 60 * sec)
            ctx.beginPath()
            ctx.moveTo(-15, 0)
            ctx.lineTo(110, 0)
            ctx.strokeStyle = '#333';
            ctx.lineWidth = 8
            ctx.stroke()
            ctx.closePath()
            ctx.restore() // 恢复上一层坐标
            ctx.save() // 存档
            // 绘制分针
            ctx.rotate(2 * Math.PI / 60 * min + 2 * Math.PI / 60 / 60 * sec)
            ctx.beginPath()
            ctx.moveTo(-20, 0)
            ctx.lineTo(130, 0)
            ctx.strokeStyle = '#888';
            ctx.lineWidth = 4
            ctx.stroke()
            ctx.closePath()
            ctx.restore() // 恢复上一层坐标
            ctx.save() // 存档
            // 绘制秒针
            ctx.rotate(2 * Math.PI / 60 * sec)
            ctx.beginPath()
            ctx.moveTo(-30, 0)
            ctx.lineTo(190, 0)
            ctx.strokeStyle = 'red';
            ctx.lineWidth = 2
            ctx.stroke()
            ctx.closePath()
            ctx.restore() // 恢复上一层坐标
 
            ctx.restore() // 恢复上一层坐标
            requestAnimationFrame(render)
        }
        render()
    </script>
</body>
