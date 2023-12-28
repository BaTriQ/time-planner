<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تنظيم الوقت</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .circle-container {
            display: flex;
            flex-direction: column-reverse;
            align-items: center;
            width: 300px;
            height: 300px;
            border-radius: 50%;
            background-color: #ecf0f1;
            overflow: hidden;
        }

        .activity {
            width: 100%;
            transition: height 0.8s ease-in-out;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            font-size: 12px;
            color: white;
            font-weight: bold;
            overflow: hidden;
        }
    </style>
</head>
<body>
    <div class="circle-container" id="circle-container">
        <!-- ستظهر المهام هنا -->
    </div>
    <label for="task">اسم المهمة:</label>
    <input type="text" id="task" placeholder="اسم المهمة">
    <label for="duration">المدة بالساعات:</label>
    <input type="number" id="duration" placeholder="المدة بالساعات">
    <button onclick="addTask()">إضافة مهمة</button>

    <script>
        const tasks = [];

        function addTask() {
            const taskName = document.getElementById("task").value;
            const taskDuration = parseFloat(document.getElementById("duration").value);
            const circleContainer = document.getElementById("circle-container");

            if (taskName && !isNaN(taskDuration) && taskDuration > 0 && taskDuration <= 24) {
                const newTask = document.createElement("div");
                newTask.className = "activity";
                newTask.style.backgroundColor = getRandomColor();
                newTask.textContent = taskName;

                tasks.push({
                    duration: taskDuration,
                    element: newTask
                });

                updateCircle();
            } else {
                alert("الرجاء إدخال بيانات صحيحة.");
            }
        }

        function getRandomColor() {
            const letters = "0123456789ABCDEF";
            let color = "#";
            for (let i = 0; i < 6; i++) {
                color += letters[Math.floor(Math.random() * 16)];
            }
            return color;
        }

        function updateCircle() {
            const circleContainer = document.getElementById("circle-container");
            circleContainer.innerHTML = "";

            tasks.forEach((task, index) => {
                const newTask = task.element.cloneNode(true);
                newTask.style.height = `${(task.duration / 24) * 100}%`;

                circleContainer.appendChild(newTask);
            });
        }
    </script>
</body>
</html>
