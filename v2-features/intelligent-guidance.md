# Intelligent Guidance System

**核心理念：主动引导用户，而不是被动回答**

## 功能设计

### 1. 智能邮件提醒系统 📧

#### 周期开始时（Day 1-3）
**邮件主题：** 🌸 Cycle [X] Started - Here's Your Personalized Plan

**内容：**
```
Hi [Name],

Your cycle just started! Based on your last 2-3 cycles, here's what to expect:

📊 YOUR CYCLE PATTERN:
- Cycle 1: 34 days, ovulation Day 16
- Cycle 2: 32 days, ovulation Day 15
- Cycle 3: [Current]

🎯 PREDICTED OVULATION:
- Most likely: Day 15-16 (Mar 24-25)
- Fertile window: Day 13-18 (Mar 22-27)
- Confidence: 85% (based on 2 cycles)

📋 YOUR ACTION PLAN:
- Day 10 (Mar 19): Watch for temperature dip
- Day 12 (Mar 21): Start LH testing (twice daily)
- Day 15 (Mar 24): Expected LH surge
- Day 17 (Mar 26): Confirm temp rise

✅ WHAT TO DO NOW:
- Check your Oura Ring is syncing daily
- Stock up on LH test strips (need ~10)
- Prepare TTC schedule with partner

I'll remind you when it's time to start LH testing!

- Kale 🥬
```

---

#### 卵泡期中期（Day 8-10）
**邮件主题：** 🔔 Heads Up: Fertile Window Approaching

**内容：**
```
Hi [Name],

You're on Day 10 - fertile window is 5-7 days away!

📊 WHAT I'M WATCHING:
✅ Temperature: -0.15°C (normal follicular range)
✅ HRV: 53 ms (stable)
⚠️ RHR: Starting to rise (normal pre-ovulation)

🌡️ TEMPERATURE CHECK:
Looking at SF weather this week... it's been warm (27-31°C).
But your body temp is actually LOWER → This is HORMONAL, not environmental! ✅

🎯 NEXT 3 DAYS:
- Watch for sudden temp dip (ovulation signal)
- If you feel different (fatigue, mood change) → That's hormones preparing
- Start checking cervical mucus daily

🧪 GET READY:
- Start LH testing in 2 days (Day 12)
- Best time: afternoon or evening (LH peaks mid-day)

Questions? Just reply to this email!

- Kale 🥬
```

---

#### LH 测试提醒（Day 12-14）
**邮件主题：** 🧪 Time to Start LH Testing!

**内容：**
```
Hi [Name],

Today is Day 12 - time to start LH testing!

📊 CURRENT SIGNALS:
✅ Temperature dipped to -0.31°C yesterday (Day 10) → PRE-OVULATION SIGNAL!
✅ HRV dropped 30% this week → Hormones shifting
⚠️ Ovulation likely in 2-4 days

🧪 LH TESTING PROTOCOL:
- Test TWICE daily (afternoon + evening)
- Don't drink water 2h before testing
- Compare test line to control line
- Take photos to track progression

📸 HOW TO READ YOUR STRIP:
- Test line LIGHTER than control = Negative (keep testing)
- Test line SAME darkness = POSITIVE! (ovulation in 24-36h)
- Test line DARKER than control = Strong positive (rare but possible)

🎯 WHAT TO WATCH FOR:
You'll see the test line get darker each day.
When it matches the control line → ALERT ME IMMEDIATELY!

I'll send partner notification and TTC timing plan.

Reply with "positive" when you get a positive test!

- Kale 🥬
```

---

#### LH 阳性后（立即发送）
**邮件主题：** 🚨 LH SURGE DETECTED - Action Required!

**内容（给用户）：**
```
Hi [Name],

🎯 LH SURGE CONFIRMED! Ovulation in 24-36 hours!

⏰ TIMING PLAN:
✅ Tonight (Day 15): TTC #1 (CRITICAL)
✅ Tomorrow morning (Day 16): TTC #2 (OPTIMAL)
✅ Tomorrow night (Day 16): TTC #3 (Optional backup)

💡 WHY THIS TIMING:
- Sperm survive 3-5 days
- Tonight's will be ready when egg releases
- Tomorrow morning = peak fertility window
- 24h spacing = optimal sperm quality

🧘 STAY RELAXED:
- No sauna/hot baths this week
- Normal exercise OK
- Avoid alcohol
- Get good sleep

📊 WHAT'S NEXT:
- Day 17-18: Temperature should rise +0.3-0.5°C
- I'll check and confirm ovulation happened
- Then we wait... 🤞

I've also emailed Michael with the timing plan!

Good luck! 🍀

- Kale 🥬
```

**邮件（给伴侣）：**
```
Subject: 🎯 Fertility Window Open - Action Plan

Hi Michael,

Winnie's LH surge just detected - optimal fertility window is NOW!

⏰ TIMING:
✅ Tonight: TTC (within next 6 hours)
✅ Tomorrow morning: TTC (24h from tonight)
✅ Tomorrow night: Optional (if energy permits)

💡 TIPS:
- Quality > quantity (24h spacing optimal)
- No alcohol tonight
- Get good rest between
- Stay positive! 😊

🚫 AVOID THIS WEEK:
- Sauna/hot tubs (kills sperm quality for months!)
- Tight underwear
- Excessive exercise

This is the best chance this cycle. You've got this! 💪

- Kale (Winnie's AI assistant) 🥬
```

---

### 2. 无模式时的主动诊断 🔍

#### 触发条件
```javascript
function detectAnomalousPattern(currentCycle, historicalCycles) {
  // Compare current to historical patterns
  const historical = historicalCycles.map(analyzeBiphasicPattern);
  const current = analyzeBiphasicPattern(currentCycle);
  
  if (historical.every(h => h.hasClearPattern) && !current.hasClearPattern) {
    return {
      anomaly: true,
      type: 'missing_biphasic_shift',
      day: currentCycle.day
    };
  }
  
  return { anomaly: false };
}
```

#### 诊断邮件（Day 14-16，无明显趋势时）
**邮件主题：** 🔍 Pattern Check: Let's Investigate Together

**内容：**
```
Hi [Name],

I noticed something different about this cycle...

📊 PATTERN COMPARISON:
Cycle 1: Clear temp shift (Day 16: -0.2°C → Day 18: +0.4°C) ✅
Cycle 2: Clear temp shift (Day 15: -0.1°C → Day 17: +0.5°C) ✅
Cycle 3: No clear shift yet (Day 15: still fluctuating)  ⚠️

🤔 POSSIBLE REASONS:
1. Ovulation delayed (might happen Day 17-20 instead)
2. Environmental factors affecting readings
3. Anovulatory cycle (no ovulation - rare but possible)

🌡️ ENVIRONMENTAL CHECK:
Let me compare your body temp with local weather...
[Analyzing SF weather Mar 10-24...]

RESULT: SF had heat wave (30°C) but your temp was LOWEST (-0.31°C)
→ Environmental factors RULED OUT ✅
→ Your patterns are real hormonal signals

🎯 QUESTIONS TO HELP ME PREDICT BETTER:

1. **LH Testing:** 
   - When did you start testing this cycle?
   - Have you seen test line getting darker?
   - Can you send photo of your strips?

2. **Physical Symptoms:**
   - Any cervical mucus changes? (egg-white texture?)
   - Breast tenderness or mild cramping?
   - Energy level or mood shifts?

3. **Lifestyle Factors:**
   - Sleep quality this week? (I see 6.5h on Day 17 - was that unusual?)
   - Stress or travel? (Can delay ovulation)
   - Exercise or diet changes?

4. **Cycle Tracking:**
   - Did you notice ovulation in Cycle 1-2? (CM, cramping, etc.)
   - Was there anything different about those cycles?

📋 NEXT STEPS:
Reply to this email with any info you have!

If no LH surge by Day 20, I recommend:
- Continue testing until Day 25
- Consider ultrasound to check follicle development
- This cycle might be longer than usual (35-40 days)

Remember: Cycle variation is normal, especially in first 3-6 months post-pill!

- Kale 🥬
```

---

### 3. 引导式提问系统 💬

#### 主动提问策略

**初次设置时：**
```
Welcome! Let's set up your fertility tracker.

QUESTION 1: Birth Control History
- Are you currently on birth control? [Yes/No]
- If recently stopped, when? [Date]
  → WHY I ASK: First 3-6 cycles post-pill can be irregular

QUESTION 2: Cycle History
- How many periods have you had since stopping BC? [Number]
- What were their dates? [Dates]
  → WHY I ASK: I need 2-3 cycles to predict accurately

QUESTION 3: Tracking Tools
- Do you have an Oura Ring? [Yes/No]
- Do you have LH test strips? [Yes/No]
- Do you track basal body temperature? [Yes/No]
  → WHY I ASK: More data = better predictions

QUESTION 4: Symptoms Awareness
- Do you notice cervical mucus changes mid-cycle? [Yes/No/Not sure]
- Do you feel ovulation (mittelschmerz cramping)? [Yes/No/Not sure]
  → WHY I ASK: Physical symptoms confirm predictions

QUESTION 5: Partner Coordination
- Who should I alert when fertile window opens? [Email]
- What timezone are you in? [TZ]
  → WHY I ASK: Timing is everything!
```

**周期中提问（引导观察）：**

**Day 8-10 邮件附加：**
```
🤔 QUICK CHECK-IN:
Help me calibrate predictions:

1. Cervical mucus today:
   [ ] Dry/sticky
   [ ] Creamy (white, lotion-like)
   [ ] Egg-white (clear, stretchy) ← FERTILE!
   [ ] Not sure how to check

2. Energy/mood:
   [ ] Normal
   [ ] More tired than usual
   [ ] Energetic
   [ ] Mood swings

3. Sleep quality (besides Oura data):
   [ ] Great
   [ ] OK
   [ ] Poor - why? __________

Reply with numbers! (e.g., "1c, 2b, 3a")
Takes 10 seconds but improves my predictions! 🎯
```

**Day 13-14 邮件附加：**
```
🧪 LH TESTING FEEDBACK:
After today's test:

1. Test line compared to control:
   [ ] Much lighter (barely visible)
   [ ] Lighter (clearly visible but faint)
   [ ] Almost same darkness ← CLOSE!
   [ ] Same or darker ← POSITIVE!

2. Compared to yesterday's test:
   [ ] Lighter
   [ ] Same
   [ ] Darker ← GOOD SIGN!

3. Photo of today's strip:
   [Attach photo] (Optional but helps!)

Reply with your answers!
If 1d or 2c → Surge is happening! 🚨
```

---

### 4. 环境因素自动检测 🌡️

#### 每日自动分析

```javascript
async function dailyEnvironmentalCheck(userLocation, date, bodyTemp) {
  // Fetch weather
  const weather = await getWeather(userLocation, date);
  
  // Correlation analysis
  const last7Days = await getWeatherHistory(userLocation, date, 7);
  const tempData = await getBodyTempHistory(date, 7);
  
  const correlation = correlate(
    last7Days.map(d => d.maxTemp),
    tempData.map(d => d.deviation)
  );
  
  // Detect anomalies
  if (Math.abs(correlation) > 0.7) {
    return {
      alert: true,
      type: correlation > 0 ? 'positive_correlation' : 'inverse_correlation',
      message: correlation > 0 ?
        "Your body temp is rising with outside temp - might be environmental!" :
        "Interesting! Outside temp is high but your body temp is low - this is hormonal!"
    };
  }
  
  return { alert: false, environmental: false };
}
```

#### 异常提醒邮件

**当检测到强环境关联时：**
```
Subject: 🌡️ Environmental Factor Alert

Hi [Name],

I noticed something about your temperature readings...

📊 PAST WEEK:
Outside temp: 18°C → 31°C (heat wave!)
Your body temp: -0.15°C → +0.05°C (rising)

⚠️ CORRELATION DETECTED: 0.78 (strong positive)

🤔 WHAT THIS MEANS:
Your body temp might be affected by:
- Room temperature while sleeping
- AC settings
- Bedding/pajamas

💡 TO GET CLEARER DATA:
- Keep bedroom temp consistent (65-68°F / 18-20°C)
- Same bedding each night
- Note if you changed AC settings

🎯 DON'T WORRY:
I'll continue tracking. Even with environmental noise,
LH testing will catch ovulation reliably!

- Kale 🥬
```

---

### 5. 学习型问答引导 🧠

#### 对话中的智能引导

**用户问："我的温度怎么这么乱？"**

**AI 回复：**
```
好问题！让我帮你分析：

首先，我需要几个信息：
1. 你最近几天睡眠环境有变化吗？
   - 室温
   - 被子厚薄
   - 空调设置

2. 对比一下上个周期的数据...
   [显示 Cycle 2 温度趋势图]
   
   上个周期在 Day 10-12 也有波动，但整体趋势是：
   - 低温期：-0.1 到 -0.2°C
   - 排卵后：+0.3 到 +0.5°C
   
   这次 Day 15 了还在 -0.1 左右波动
   → 可能排卵还没发生

3. 让我检查一下是不是环境影响...
   [自动运行天气对比]
   
   结果：SF 这周 30°C 热浪，但你体温反而最低
   → 不是环境因素！是真实的荷尔蒙信号 ✅

所以回答你的问题：
温度"乱"是因为还在卵泡期，等排卵后会看到明显上升。

👉 建议：继续测 LH，预计 Day 16-18 会看到阳性。
```

**用户问："精子会不会死了？"**

**AI 回复：**
```
不会！让我算给你看：

精子存活时间（科学数据）：
- 24h: 90% 活力 ✅
- 48h: 80% 活力 ✅
- 72h: 70% 活力 ✅
- 96h: 50% 活力 ⚠️
- 120h: 30% 活力 ⚠️

你的情况：
- 今早（Day 15）TTC
- 现在 LH 阳性（晚上）
- 预计排卵：明晚或后天（Day 16-17）

时间差：24-48 小时
→ 精子活力：80-90% ✅✅✅

而且，精子需要时间游到输卵管（6-12h）
+ 需要"获能"才能受精（12-24h）
→ 提前 24-48h 到达 = 完美 timing! 🎯

👉 建议：明早再 TTC 一次（保险）
```

---

## 实现优先级

### Phase 1: 核心提醒系统（MVP）
- [x] 周期开始邮件
- [x] Day 10 准备提醒
- [x] Day 12 LH 测试提醒
- [x] LH 阳性即时通知（用户 + 伴侣）

### Phase 2: 智能诊断
- [x] 无模式检测
- [x] 环境因素分析
- [x] 主动提问引导

### Phase 3: 高级功能
- [ ] 图像识别 LH 试纸
- [ ] 预测模型机器学习
- [ ] 多用户数据对比

---

## 配置示例

```json
{
  "notifications": {
    "email": {
      "user": "winnie@example.com",
      "partner": "michael@example.com",
      "enabled": true
    },
    "triggers": {
      "cycleStart": true,
      "day10Alert": true,
      "lhTestReminder": true,
      "lhPositive": true,
      "ovulationConfirmed": true,
      "anomalyDetected": true
    }
  },
  "intelligence": {
    "environmentalCheck": true,
    "guidedQuestions": true,
    "patternComparison": true,
    "location": "San Francisco, CA"
  }
}
```

---

**这套系统的核心：不是被动回答问题，而是主动发现问题、引导用户提供关键信息、在正确的时间问正确的问题！** 🎯

准备实现吗？🥬
