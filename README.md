
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة اختبار قوة كلمة المرور</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 30px;
            background-color: #f5f5f5;
        }

        .container {
            width: 320px;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            background-color: #fff;
            text-align: center;
        }

        .password-input {
            width: 100%;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 5px;
            margin-bottom: 10px;
        }

        .strength-bar {
            height: 10px;
            border-radius: 5px;
            margin-top: 10px;
            background-color: #ddd;
            overflow: hidden;
        }

        .strength-bar-fill {
            height: 100%;
            transition: width 0.3s ease;
        }

        .feedback {
            margin-top: 10px;
            font-weight: bold;
        }

        .checklist {
            text-align: left;
            font-size: 14px;
            color: #555;
            margin-top: 10px;
        }

        .checklist-item {
            margin: 5px 0;
        }

        .checklist-item.valid {
            color: green;
            font-weight: bold;
        }

        .copy-btn {
            margin-top: 15px;
            padding: 10px 20px;
            font-size: 14px;
            color: white;
            background-color: #4CAF50;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            display: none;
        }

        .copy-btn:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <!-- Arabic Introduction -->
    <div class="container" style="margin-bottom: 20px;">
        <p><strong>أداة اختبار قوة كلمة المرور</strong> تساعد المستخدمين على إنشاء كلمات مرور أكثر أمانًا من خلال تقديم ملاحظات فورية حول معايير الأمان الأساسية، مثل الطول، واستخدام الأحرف الكبيرة والصغيرة، والأرقام، والرموز الخاصة. يوفر شريط قوة بصري وقائمة مرجعية ترشد المستخدمين لتحسين كلمات المرور، مع تحديثات ديناميكية تتدرج من "ضعيفة جدًا" إلى "قوية جدًا" أثناء الكتابة.</p>
        <p>بمجرد أن تكون كلمة المرور قوية، يظهر زر <strong>نسخ كلمة المرور</strong> لسهولة النسخ إلى الحافظة. تساعد هذه الأداة في تعزيز ممارسات كلمات المرور الآمنة، مما يمكّن المستخدمين من حماية حساباتهم من خلال ملاحظات واضحة وقابلة للتنفيذ.</p>
    </div>

    <div class="container">
        <h2>أداة اختبار قوة كلمة المرور</h2>
        <input type="password" id="passwordInput" class="password-input" placeholder="أدخل كلمة المرور">
        <div class="strength-bar">
            <div id="strengthBarFill" class="strength-bar-fill"></div>
        </div>
        <div id="feedback" class="feedback">أدخل كلمة المرور</div>
        
        <!-- Checklist for password requirements -->
        <div class="checklist">
            <p class="checklist-item" id="lengthCheck">❌ على الأقل 8 أحرف</p>
            <p class="checklist-item" id="uppercaseCheck">❌ على الأقل حرف كبير واحد</p>
            <p class="checklist-item" id="lowercaseCheck">❌ على الأقل حرف صغير واحد</p>
            <p class="checklist-item" id="numberCheck">❌ على الأقل رقم واحد</p>
            <p class="checklist-item" id="specialCharCheck">❌ على الأقل رمز خاص واحد</p>
        </div>
        
        <!-- Copy to clipboard button -->
        <button id="copyBtn" class="copy-btn" onclick="copyPassword()">نسخ كلمة المرور</button>
    </div>

    <script>
        document.getElementById("passwordInput").addEventListener("input", checkPasswordStrength);

        function checkPasswordStrength() {
            const password = document.getElementById("passwordInput").value;
            const strengthBarFill = document.getElementById("strengthBarFill");
            const feedback = document.getElementById("feedback");
            const copyBtn = document.getElementById("copyBtn");

            let strength = 0;

            // Check requirements
            const lengthCheck = password.length >= 8;
            const uppercaseCheck = /[A-Z]/.test(password);
            const lowercaseCheck = /[a-z]/.test(password);
            const numberCheck = /[0-9]/.test(password);
            const specialCharCheck = /[^A-Za-z0-9]/.test(password);

            // Update checklist based on requirements
            document.getElementById("lengthCheck").className = lengthCheck ? "checklist-item valid" : "checklist-item";
            document.getElementById("lengthCheck").textContent = lengthCheck ? "✔️ على الأقل 8 أحرف" : "❌ على الأقل 8 أحرف";
            
            document.getElementById("uppercaseCheck").className = uppercaseCheck ? "checklist-item valid" : "checklist-item";
            document.getElementById("uppercaseCheck").textContent = uppercaseCheck ? "✔️ على الأقل حرف كبير واحد" : "❌ على الأقل حرف كبير واحد";
            
            document.getElementById("lowercaseCheck").className = lowercaseCheck ? "checklist-item valid" : "checklist-item";
            document.getElementById("lowercaseCheck").textContent = lowercaseCheck ? "✔️ على الأقل حرف صغير واحد" : "❌ على الأقل حرف صغير واحد";
            
            document.getElementById("numberCheck").className = numberCheck ? "checklist-item valid" : "checklist-item";
            document.getElementById("numberCheck").textContent = numberCheck ? "✔️ على الأقل رقم واحد" : "❌ على الأقل رقم واحد";
            
            document.getElementById("specialCharCheck").className = specialCharCheck ? "checklist-item valid" : "checklist-item";
            document.getElementById("specialCharCheck").textContent = specialCharCheck ? "✔️ على الأقل رمز خاص واحد" : "❌ على الأقل رمز خاص واحد";

            // Calculate strength
            if (lengthCheck) strength += 1;
            if (uppercaseCheck) strength += 1;
            if (lowercaseCheck) strength += 1;
            if (numberCheck) strength += 1;
            if (specialCharCheck) strength += 1;

            let strengthText;
            let color;

            switch (strength) {
                case 0:
                case 1:
                    strengthText = "ضعيفة جداً";
                    color = "red";
                    strengthBarFill.style.width = "20%";
                    break;
                case 2:
                    strengthText = "ضعيفة";
                    color = "orange";
                    strengthBarFill.style.width = "40%";
                    break;
                case 3:
                    strengthText = "متوسطة";
                    color = "yellow";
                    strengthBarFill.style.width = "60%";
                    break;
                case 4:
                    strengthText = "قوية";
                    color = "lightgreen";
                    strengthBarFill.style.width = "80%";
                    break;
                case 5:
                    strengthText = "قوية جداً";
                    color = "green";
                    strengthBarFill.style.width = "100%";
                    break;
            }

            feedback.textContent = strengthText;
            feedback.style.color = color;
            strengthBarFill.style.backgroundColor = color;

            // Show copy button if password is strong or very strong
            copyBtn.style.display = (strength >= 4) ? "inline-block" : "none";
        }

        // Copy password to clipboard
        function copyPassword() {
            const password = document.getElementById("passwordInput").value;
            navigator.clipboard.writeText(password).then(() => {
                alert("تم نسخ كلمة المرور إلى الحافظة!");
            });
        }
    </script>
</body>
</html>
