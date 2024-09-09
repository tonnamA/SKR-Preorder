<!DOCTYPE html>
<html>
<head>
<title>คำนวณแคลลอรี่</title>
<meta charset="UTF-8">
<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f9;
  color: #333;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  color: #4CAF50;
}

label {
  display: block;
  margin-bottom: 10px;
  font-weight: bold;
}

input[type="number"], select {
  width: 100%;
  padding: 10px;
  margin: 8px 0;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  background-color: #4CAF50;
  color: white;
  border: none;
  padding: 15px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 10px 0;
  cursor: pointer;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #45a049;
}

h2 {
  color: #333;
}

table {
  border-collapse: collapse;
  width: 100%;
  margin-top: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 12px;
  text-align: left;
}

th {
  background-color: #4CAF50;
  color: white;
}

td {
  background-color: #f9f9f9;
}

ul {
  list-style-type: none;
  padding: 0;
}

ul li {
  background: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 10px;
  margin-bottom: 10px;
}
</style>
</head>
<body>

<div class="container">
  <h1>คำนวณแคลลอรี่</h1>

  <label for="currentWeight">น้ำหนักปัจจุบัน (กิโลกรัม):</label>
  <input type="number" id="currentWeight" name="currentWeight">

  <label for="targetWeight">น้ำหนักเป้าหมาย (กิโลกรัม):</label>
  <input type="number" id="targetWeight" name="targetWeight">

  <label for="height">ความสูง (เซนติเมตร):</label>
  <input type="number" id="height" name="height">

  <label for="age">อายุ (ปี):</label>
  <input type="number" id="age" name="age">

  <label for="gender">เพศ:</label>
  <select id="gender">
    <option value="male">ชาย</option>
    <option value="female">หญิง</option>
  </select>

  <label for="activityLevel">ระดับกิจกรรม:</label>
  <select id="activityLevel">
    <option value="1.2">Sedentary (นั่งทำงานส่วนใหญ่)</option>
    <option value="1.375">Lightly active (ออกกำลังกายเบาๆ)</option>
    <option value="1.55">Moderately active (ออกกำลังกายปานกลาง)</option>
    <option value="1.725">Very active (ออกกำลังกายหนัก)</option>
    <option value="1.9">Super active (ออกกำลังกายหนักมาก)</option>
  </select>

  <button onclick="calculateCalories()">คำนวณ</button>

  <div id="results" style="display:none;">
    <h2>ผลลัพธ์</h2>
    <p id="calorieIntake"></p>
    
    <h2>ตัวอย่างเมนูอาหาร</h2>
    <table>
      <thead>
        <tr>
          <th>มื้ออาหาร</th>
          <th>เมนู</th>
          <th>แคลอรี่</th>
        </tr>
      </thead>
      <tbody id="mealPlan">
      </tbody>
    </table>

    <h2>คำแนะนำการออกกำลังกาย</h2>
    <ul>
      <li>วิ่งเหยาะๆ 30 นาที ลดได้ประมาณ 250-350 แคลอรี่</li>
      <li>ว่ายน้ำ 30 นาที ลดได้ประมาณ 200-300 แคลอรี่</li>
      <li>ปั่นจักรยาน 30 นาที ลดได้ประมาณ 150-250 แคลอรี่</li>
    </ul>
  </div>
</div>
<script>
  const foodData = {
    "ไข่ดาว": 112,
    "ไข่เจียว": 600,
    "ไข่ตุ๋น": 72,
    "ไข่ต้ม": 80,
    "ข้าวมันไก่ต้ม": 585,
    "ข้าวมันไก่ทอด": 695,
    "ข้าวมันไก่ยำ": 640,
    "ข้าวไก่พิซซ่า": 530,
    "ข้าวไก่แซ่บ": 620,
    "ข้าวไก่ชีส": 600,
    "ข้าวไก่ห่อสาหร่าย": 883,
    "คั่วกลิ้ง": 140,
    "ข้าวกะเพราหมูสับ": 630,
    "ข้าวผัด": 550,
    "ข้าวหมูแดง": 540,
    "ข้าวหมุกระเทียม": 525,
    "ข้าวแกงกะหรี่": 880,
    "ข้าวปลาดอรี่": 200,
    "แกงเขียวหวาน": 90,
    "ต้มขาไก่": 1034.3,
    "มัสมั่นไก่": 580,
    "ปลาหมึกทอด": 175,
    "หมูทอด": 405.1,
    "ราดหน้าเส้นใหญ่": 500,
    "ผัดซีอิ๊วเส้นใหญ่": 675,
    "ก๋วยเตี๋ยวต้มยำ": 310,
    "ก๋วยเตี๋ยวน้ำใส": 140,
    "ก๋วยเตี๋ยวน้ำตก": 180,
    "เส้นหมี่": 168,
    "เส้นบะหมี่": 280,
    "เส้นใหญ่": 160,
    "เส้นเล็ก": 180,
    "สุกี้หมูเด้งวุ้นเส้น": 467,
    "สปาเก้ตตี้คาโบนาร่า": 317,
    "ผัดมักกะโรนี": 532.7,
    "ข้าวไข่เจียวหมูสับ": 600 
  };
function calculateBMR(weight, height, age, gender) {
  if (gender === 'male') {
    return 10 * weight + 6.25 * height - 5 * age + 5; //สูตรหาน้ำหนักผู้ชาย
  } else {
    return 10 * weight + 6.25 * height - 5 * age - 161; //ผู้หญิง
  }
}

function calculateCalories() {
  const currentWeight = parseFloat(document.getElementById("currentWeight").value);
  const targetWeight = parseFloat(document.getElementById("targetWeight").value);
  const height = parseFloat(document.getElementById("height").value);
  const age = parseFloat(document.getElementById("age").value);
  const gender = document.getElementById("gender").value;
  const activityLevel = parseFloat(document.getElementById("activityLevel").value);
  
  if (isNaN(currentWeight) || isNaN(targetWeight) || isNaN(height) || isNaN(age)) {
    alert("กรุณากรอกข้อมูลให้ครบถ้วน");
    return;
  }

  let bmr = calculateBMR(currentWeight, height, age, gender);
  let calorieIntake = bmr * activityLevel;
  
  if (targetWeight < currentWeight) {
    calorieIntake -= 500; 
  } else if (targetWeight > currentWeight) {
    calorieIntake += 500;
  }

  console.log(`Current Weight: ${currentWeight}, Target Weight: ${targetWeight}, Calorie Intake: ${calorieIntake}`);

  document.getElementById("calorieIntake").innerHTML = `คุณควรบริโภคแคลอรี่ประมาณ ${Math.round(calorieIntake)} แคลอรี่ต่อวัน`;
  document.getElementById("results").style.display = "block";

  generateMealPlan(calorieIntake);
}

function generateMealPlan(calorieTarget) {
  const meals = {
    "เช้า": { target: calorieTarget * 0.3 },
    "กลางวัน": { target: calorieTarget * 0.4 },
    "เย็น": { target: calorieTarget * 0.3 }
  };

  let mealPlanHTML = "";

  for (const meal in meals) {
    let calorieSum = 0;
    let foodItems = [];
    let iterations = 0; // Counter to prevent infinite loop
    const maxIterations = 100; // Maximum iterations to avoid infinite loop

    while (calorieSum < meals[meal].target && iterations < maxIterations) {
      iterations++;
      const randomFood = Object.keys(foodData)[Math.floor(Math.random() * Object.keys(foodData).length)];
      const foodCalories = foodData[randomFood];

      // Ensure we do not exceed the target
      if (calorieSum + foodCalories <= meals[meal].target) {
        calorieSum += foodCalories;
        foodItems.push({ name: randomFood, calories: foodCalories });
      }
    }

    // If iterations exceed maximum, we may have a problem
    if (iterations >= maxIterations) {
      console.warn(`Reached maximum iterations for ${meal}. Consider adjusting your calorie targets.`);
    }

    foodItems.forEach(item => {
      mealPlanHTML += `<tr><td>${meal}</td><td>${item.name}</td><td>${item.calories}</td></tr>`;
    });
  }

  document.getElementById("mealPlan").innerHTML = mealPlanHTML;
}
</script>

</body>
</html>
