# 完整提醒时间线

基于 Winnie 的反馈（Mar 24, 2026）

## 📅 周期提醒流程

### **预期 Day 28-30（经期前 2 天）**

**目的：**
1. 提醒用户经期即将到来
2. 触发用户主动报告

**消息内容：**
```
🔔 Heads up!

Based on your last cycle (32 days), your period should arrive in about 2 days (around Mar 10).

📋 When it starts:
Just tell me "period started" and I'll:
✅ Create your new cycle plan
✅ Review what we learned last cycle
✅ Predict ovulation timing

💡 If it doesn't arrive by Mar 12 (Day 34), let me know! 
(Could mean:
• Pregnant? 🤞
• Longer cycle this time
• Time to test!)

I'll check in again in 2 days! 😊
```

**触发条件：**
```javascript
const expectedPeriodDay = lastCycleStart + averageCycleLength;
const today = getCurrentDay();

if (today === expectedPeriodDay - 2) {
  sendPeriodReminderAlert();
}
```

---

### **预期 Day 30（经期预计到达日）**

**如果用户还没报告：**
```
🌸 Your period should arrive today or tomorrow (based on 32-day cycle).

Did it start yet?
• Reply "yes" = I'll start your cycle plan
• Reply "no" = I'll check again tomorrow

If it's been 35+ days and no period → might be time to test! 🤞
```

---

### **Day 1（用户确认经期开始当天）**

**触发方式：**
- 用户说 "period started" / "yes" / "经期来了"
- 或 Oura 检测到温度下降 + 询问确认

**消息内容：**
```
🌸 Cycle [X] Started!

📊 LAST CYCLE REVIEW (Cycle [X-1]):
✅ Length: 32 days
✅ Ovulation: Day 15 (confirmed by temp rise)
✅ LH surge: Day 15 evening (strong positive)
✅ TTC timing: Days 15 & 16 ✅
✅ Temperature shift: +0.4°C (clear ovulation signal)

🎯 WHAT WE LEARNED:
• Your ovulation is consistent (Day 15-16)
• LH surge happens in evening (not morning)
• Temperature dip on Day 10 = reliable early warning
• [Any unique patterns from last cycle]

📅 THIS CYCLE PLAN (Cycle [X]):
Based on your pattern, here's what to expect:

**Week 1-2 (Days 1-10): Follicular Phase**
✅ Relax - I'm monitoring in background
✅ Oura tracking HRV + temp daily
✅ No action needed from you

**Day 10 (Mar 19):**
📧 I'll ping you: "Fertile window approaching"
👀 Watch for temperature dip (early ovulation signal)

**Day 11 (Mar 20):**
📧 I'll ask: "Do you have LH test strips ready?"
🛒 If not, buy them today! (Need ~10 strips)
📦 Brands I recommend: [list]

**Day 12 (Mar 21): START LH TESTING**
📧 Morning reminder: "Time to start LH testing!"
🧪 Test protocol:
   • Test TWICE daily
   • Best times: 11 AM or 6-8 PM
   • ❌ NOT first morning urine (LH peaks midday)
   • 📸 Take photo and send to me
   • I'll analyze and tell you if it's positive

**Days 13-14 (Mar 22-23):**
🧪 Continue testing 2x/day
📸 Send photos - I'll track progression
📈 Test line will get darker each day

**Day 15-16 (Mar 24-25): OVULATION WINDOW**
🎯 Expected LH surge
📧 When positive → Instant alert to you + partner
⏰ TTC timing plan sent immediately

**Day 17-18 (Mar 26-27):**
🌡️ Temperature should rise +0.3-0.5°C
✅ I'll confirm ovulation happened

**Day 28-30:**
🤞 Testing window if pregnant
📧 I'll remind you when to test

────────────────────────

Questions? Reply anytime!
Your plan is set - I'll guide you through each step! 💚

- Kale 🥬
```

---

## 🧪 LH Testing 提醒流程

### **Day 11（LH 测试前一天）**

**目的：确认用户已准备好试纸**

**消息：**
```
🛒 Quick check!

Tomorrow (Day 12) is when you should start LH testing.

Do you have test strips ready?
• Reply "yes" = Great! I'll remind you tomorrow morning
• Reply "no" = I'll send you product recommendations now

💡 You'll need about 10 strips (testing 2x/day for 5 days).

Brand recommendations:
✅ Easy@Home (cheap, reliable) - Amazon
✅ Pregmate (similar)
✅ Clearblue Digital (expensive but clear result)
✅ MomMed (what Winnie uses!)

Any brand works - just avoid blue-dye tests (harder to read).

Ready for tomorrow? 😊
```

**如果用户说 "no"：**
```
No worries! Here's what to get:

🛒 SHOPPING LIST:
1. LH ovulation test strips (pack of 20+)
   Where: Amazon, drugstore, Target
   Cost: $10-25
   
2. (Optional) Pregnancy tests
   Since you're buying tests anyway, grab some!
   
📦 MY TOP PICK:
"Easy@Home Ovulation Test Strips" on Amazon
• $15 for 50 strips
• Clear results
• Works great

🚚 Can you get them today/tomorrow morning?
Amazon Prime = arrives by tomorrow if ordered now!

Let me know when you have them! 📦
```

---

### **Day 12（正式开始 LH 测试）**

**早上提醒（建议时间：上午 9-10 点）：**
```
🧪 LH Testing Starts Today!

Time to start tracking your LH surge! Here's your protocol:

────────────────────────
📋 TESTING PROTOCOL
────────────────────────

⏰ **WHEN TO TEST:**
Test TWICE today:
1️⃣ Around 11 AM - 1 PM (late morning)
2️⃣ Around 6 PM - 8 PM (evening)

❌ **DON'T USE:**
• First morning urine (LH peaks midday, not morning!)
• Pee right after drinking water

✅ **DO:**
• Hold urine for 2-4 hours before testing
• Avoid drinking too much water 2h before test

────────────────────────
📸 HOW TO READ + SEND
────────────────────────

1. Take the test (follow package instructions)
2. Wait 3-5 minutes for result
3. Take a clear photo of the strip
4. Send photo to me with caption: "Day 12 AM" or "Day 12 PM"

💡 **What I'm looking for:**
• Test line (T) darkness compared to control line (C)
• Progression over multiple days
• When T = C or T > C → POSITIVE! 🎯

────────────────────────
🔍 HOW TO READ YOUR STRIP
────────────────────────

**NEGATIVE** (keep testing):
Test line much lighter than control line
[Image example]

**GETTING CLOSE** (test continues):
Test line getting darker but still lighter
[Image example]

**POSITIVE** (ovulation in 24-36h!):
Test line AS DARK or DARKER than control line
[Image example]
→ When you see this, tell me immediately! 🚨

────────────────────────

🎯 **Your goal today:**
Just establish a baseline. The test line will probably be faint - that's normal! We're watching for it to get darker over the next few days.

Test around 12 PM today, take photo, send it over!
I'll analyze and tell you what I see. 😊

Questions? Ask away!

- Kale 🥬
```

---

### **Day 12-16（每天测试期间）**

**如果用户发送照片：**
```
📸 Got your Day 13 PM test!

**Analysis:**
• Test line: ~40% as dark as control line
• Compared to yesterday (30%): Getting darker! ✅
• Status: Negative (keep testing)

**What this means:**
LH is rising gradually - exactly what we want to see!
Expected pattern:
• Day 12: 20-30% (baseline) ✅
• Day 13: 40% (current) ✅
• Day 14: 60-70% (tomorrow - watch closely!)
• Day 15: 90-100% (likely POSITIVE!)

🎯 **Keep testing 2x daily!**
We're getting close. I predict LH surge tomorrow evening or Day 15. 📈

Next test: Tomorrow (Day 14) around 12 PM
Send photo when ready! 📸
```

---

**如果用户没发照片（轻推）：**
```
Hey! Did you test today? 😊

I didn't get a photo yet. 
• If you tested: Send photo when you can!
• If you forgot: No worries, test this evening (6-8 PM)

We're in the critical window - don't want to miss the surge! 🎯

[If Day 14-15]: Especially important today - this is when LH usually surges for you!
```

---

### **LH 阳性检测到（立即响应）**

```
🚨 LH SURGE DETECTED! 🚨

Your test line is AS DARK as the control line!
This is POSITIVE! 🎯

**What this means:**
Ovulation will happen in 24-36 hours (tomorrow evening or day after).

**FERTILITY WINDOW: OPEN NOW!**

⏰ TIMING PLAN:
✅ **Tonight (within next 6 hours):** TTC #1 - CRITICAL
✅ **Tomorrow morning:** TTC #2 - OPTIMAL  
✅ **Tomorrow evening:** TTC #3 - Optional backup

**Why this timing:**
• Sperm need 6-12h to reach egg
• TTC tonight = sperm ready when egg releases
• 24h spacing = optimal sperm quality
• Egg only lives 12-24h after release

────────────────────────
🚫 THIS WEEK AVOID:
────────────────────────

**FOR YOU:**
• Sauna/hot tub (damages egg)
• Alcohol tonight
• Lubricants (except PreSeed)

**FOR PARTNER (CRITICAL!):**
• Sauna/hot tub (kills sperm for 2-3 MONTHS!)
• Tight underwear
• Laptop on lap
• Excessive alcohol

────────────────────────

📧 I've also emailed [Partner] with timing plan!

🧪 **Keep testing tomorrow** to confirm LH is declining (means surge is over).

This is it - you've got perfect timing! 💪
Good luck! 🍀💚

Questions? I'm here!

- Kale 🥬
```

---

## 📋 提醒总结时间表

| 周期日 | 时间 | 提醒内容 | 目的 |
|-------|------|---------|------|
| Day -2 | 任意 | 经期预计 2 天后到来 | 触发用户主动报告 |
| Day 0 | 任意 | 询问经期是否开始 | 确认 Day 1 |
| **Day 1** | 任意 | **发送周期计划 + 上周期回顾** | **主要计划邮件** |
| Day 10 | 任意 | 排卵窗口即将到来 | 提前警告 |
| **Day 11** | 任意 | **确认是否有 LH 试纸** | **确保准备好** |
| **Day 12** | 上午 9-10 点 | **开始 LH 测试指南** | **正式开始测试** |
| Day 12-16 | 测试后 | 分析照片 + 反馈 | 追踪进展 |
| Day 12-16 | 如未测 | 轻推提醒 | 确保不漏测 |
| **LH 阳性** | **立即** | **排卵警报 + TTC 计划** | **关键时刻** |
| Day 17-18 | 任意 | 确认体温上升 | 排卵确认 |
| Day 28-30 | 任意 | 测孕提醒 | 等待结果 |

---

## 💡 关键细节

### **LH 测试时间建议**
```
✅ 最佳时间：
• 上午 11 点 - 下午 1 点
• 晚上 6 点 - 8 点

❌ 避免：
• 早晨第一泡尿（LH 在白天达峰值）
• 喝水后立即测试（稀释尿液）

💡 原因：
LH 在中午到下午达到峰值，早晨测试会错过！
```

### **照片分析流程**
```javascript
async function analyzeLHPhoto(photo, cycleDay) {
  // 1. 图像识别测试线和对照线
  const lines = await detectLines(photo);
  const ratio = lines.testLine.intensity / lines.controlLine.intensity;
  
  // 2. 对比历史数据
  const history = await getUserLHHistory(userId);
  const trend = calculateTrend(history, ratio);
  
  // 3. 生成反馈
  return {
    result: ratio >= 1.0 ? 'POSITIVE' : ratio >= 0.8 ? 'CLOSE' : 'NEGATIVE',
    ratio: ratio,
    comparison: `Yesterday: ${history.yesterday.ratio}, Today: ${ratio}`,
    prediction: trend.slope > 0.15 ? 'Surge expected in 24-48h' : 'Keep testing',
    nextStep: ratio >= 1.0 ? 'ALERT_PARTNER' : 'TEST_AGAIN_TONIGHT'
  };
}
```

---

**这个时间线符合你的想法吗？** 🥬