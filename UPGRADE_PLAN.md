# Fertility Tracker v2.0 - Upgrade Plan

Based on successful Cycle 3 prediction (Mar 2026)

## New Features from Real-World Success

### 1. Environmental Temperature Correlation ✅
**Problem:** Body temp fluctuations could be from room temperature
**Solution:** Fetch local weather data and correlate with body temp deviations
**Implementation:**
```javascript
async function analyzeEnvironmentalFactors(location, dates, bodyTemps) {
  const weather = await fetchWeatherHistory(location, dates);
  const correlation = correlate(weather.temps, bodyTemps);
  
  if (correlation > 0.7) {
    return { environmental: true, confidence: correlation };
  }
  return { hormonal: true, evidence: "inverse correlation" };
}
```

**Example:** SF heat wave (27-31°C) coincided with Winnie's LOWEST body temp (-0.31°C) → confirmed hormonal signal, not environmental.

---

### 2. Temperature Trend Pattern Recognition ✅
**Problem:** User notices "no clear trend" but agent doesn't catch it
**Solution:** Compare current cycle temp pattern to previous cycles

**Implementation:**
```javascript
async function analyzeTempTrend(currentCycle, historicalCycles) {
  const currentPattern = detectBiphasicPattern(currentCycle);
  const historicalPattern = historicalCycles.map(detectBiphasicPattern);
  
  if (!currentPattern.hasClearShift && historicalPattern.every(p => p.hasClearShift)) {
    return {
      alert: "Current cycle lacks biphasic pattern seen in previous cycles",
      recommendation: "Monitor closely, consider ultrasound confirmation"
    };
  }
}

function detectBiphasicPattern(temps) {
  const follicular = temps.slice(0, 14);
  const luteal = temps.slice(14);
  const avgFollicular = mean(follicular);
  const avgLuteal = mean(luteal);
  
  return {
    hasClearShift: (avgLuteal - avgFollicular) >= 0.3,
    shiftMagnitude: avgLuteal - avgFollicular
  };
}
```

---

### 3. LH Test Strip Image Analysis ✅
**Problem:** Manual LH interpretation is subjective
**Solution:** Use image analysis to quantify test line darkness

**Implementation:**
```javascript
const { analyzeImage } = require('opencv4nodejs');

async function analyzeLHStrip(imagePath) {
  const img = await analyzeImage(imagePath);
  const controlLine = detectLine(img, 'control');
  const testLine = detectLine(img, 'test');
  
  const ratio = testLine.intensity / controlLine.intensity;
  
  if (ratio >= 1.0) return { result: 'positive', ratio, confidence: 0.95 };
  if (ratio >= 0.8) return { result: 'near-positive', ratio, confidence: 0.85 };
  if (ratio >= 0.5) return { result: 'rising', ratio, confidence: 0.75 };
  return { result: 'negative', ratio, confidence: 0.9 };
}
```

**Bonus:** Track progression over multiple days
```javascript
function trackLHProgression(dailyResults) {
  const ratios = dailyResults.map(r => r.ratio);
  const trend = linearRegression(ratios);
  
  if (trend.slope > 0.1) {
    return { status: 'rising', peakExpected: estimatePeakDay(trend) };
  }
}
```

---

### 4. Sperm Survival Timeline Calculator ✅
**Problem:** User worried if "sperm will still be alive"
**Solution:** Calculate optimal TTC timing based on sperm survival curves

**Implementation:**
```javascript
function calculateFertilityWindow(lhSurgeDay, lastTTC) {
  const spermSurvival = [
    { hours: 24, viability: 0.9, fertility: 0.95 },
    { hours: 48, viability: 0.8, fertility: 0.85 },
    { hours: 72, viability: 0.7, fertility: 0.70 },
    { hours: 96, viability: 0.5, fertility: 0.50 },
    { hours: 120, viability: 0.3, fertility: 0.30 }
  ];
  
  const hoursSinceT TC = (lhSurgeDay - lastTTC) * 24;
  const survival = spermSurvival.find(s => s.hours >= hoursSinceTTC);
  
  return {
    spermViability: survival.viability,
    fertilityPotential: survival.fertility,
    recommendation: survival.viability > 0.7 ? 
      "Good timing - sperm viable" : 
      "Consider TTC again for optimal coverage"
  };
}
```

**Optimal frequency calculator:**
```javascript
function recommendTTCSchedule(lhPeakDay) {
  return [
    { day: lhPeakDay - 2, priority: 'high', reason: 'Sperm ready when ovulation occurs' },
    { day: lhPeakDay, priority: 'critical', reason: 'LH peak - ovulation 24-36h away' },
    { day: lhPeakDay + 1, priority: 'high', reason: 'Ovulation window coverage' },
    { day: lhPeakDay + 2, priority: 'optional', reason: 'Late ovulation backup' }
  ];
}
```

---

### 5. Oura Data Parser Fix ✅
**Problem:** Contributor scores (0-100) were being read as actual BPM/ms
**Solution:** Parse actual values from correct endpoints

**Implementation:**
```javascript
async function getActualOuraMetrics(token, startDate, endDate) {
  // WRONG: Using daily_readiness contributor scores
  // const readiness = await fetch('daily_readiness');
  // const rhr = readiness.contributors.resting_heart_rate; // This is a SCORE!
  
  // CORRECT: Using sleep endpoint for actual values
  const sleep = await fetch(`sleep?start_date=${startDate}&end_date=${endDate}`, {
    headers: { Authorization: `Bearer ${token}` }
  });
  
  return sleep.data.map(night => ({
    date: night.day,
    actualRHR: night.lowest_heart_rate,  // Actual BPM
    actualHRV: night.average_hrv,         // Actual ms
    sleepDuration: night.total_sleep_duration / 3600, // Convert to hours
    deepSleep: night.deep_sleep_duration / 3600,
    remSleep: night.rem_sleep_duration / 3600
  }));
}

async function getActualTemperature(token, startDate, endDate) {
  const readiness = await fetch(`daily_readiness?start_date=${startDate}&end_date=${endDate}`);
  
  return readiness.data.map(day => ({
    date: day.day,
    tempDeviation: day.temperature_deviation,  // Actual °C deviation
    tempTrend: day.temperature_trend_deviation // Trend in °C
  }));
}
```

---

## Enhanced Prediction Algorithm

**Multi-Signal Fusion:**
```javascript
async function predictOvulation(cycleDay, ouraData, lhHistory, weatherData) {
  const signals = [];
  
  // Signal 1: Temperature dip (Day 10-14)
  const tempDip = detectTempDip(ouraData.temperature);
  if (tempDip.detected && tempDip.day >= 10 && tempDip.day <= 14) {
    signals.push({
      type: 'temp_dip',
      confidence: 0.7,
      ovulationETA: tempDip.day + 2  // Ovulation 2 days after dip
    });
  }
  
  // Signal 2: HRV drop
  const hrvDrop = detectHRVDrop(ouraData.hrv);
  if (hrvDrop.magnitude > 0.3) {  // >30% drop
    signals.push({
      type: 'hrv_drop',
      confidence: 0.6,
      ovulationETA: hrvDrop.day + 3
    });
  }
  
  // Signal 3: LH surge
  const lhSurge = detectLHSurge(lhHistory);
  if (lhSurge.detected) {
    signals.push({
      type: 'lh_surge',
      confidence: 0.95,
      ovulationETA: lhSurge.day + 1.5  // 24-36 hours
    });
  }
  
  // Signal 4: Environmental correlation check
  const envCheck = await analyzeEnvironmentalFactors(weatherData, ouraData.temperature);
  if (!envCheck.environmental) {
    // Boost confidence of temp/HRV signals
    signals.forEach(s => {
      if (s.type === 'temp_dip' || s.type === 'hrv_drop') {
        s.confidence *= 1.2;
      }
    });
  }
  
  // Weighted average prediction
  const prediction = signals.reduce((acc, sig) => {
    acc.ovulationDay += sig.ovulationETA * sig.confidence;
    acc.totalConfidence += sig.confidence;
    return acc;
  }, { ovulationDay: 0, totalConfidence: 0 });
  
  return {
    predictedDay: Math.round(prediction.ovulationDay / prediction.totalConfidence),
    confidence: Math.min(prediction.totalConfidence, 1.0),
    signals: signals
  };
}
```

---

## User Interaction Improvements

### Conversational Guidance

Based on Winnie's questions during Cycle 3:

**Q: "Will sperm still be alive by ovulation?"**
```javascript
if (userAsksAboutSpermViability) {
  const timing = calculateFertilityWindow(lhSurgeDay, lastTTCDay);
  return `
Yes! Sperm can survive 3-5 days in ideal conditions.
You had TTC ${timing.hoursSince}h ago.
Sperm viability: ${timing.viability * 100}%
Fertility potential: ${timing.fertility * 100}%
Recommendation: ${timing.recommendation}
  `;
}
```

**Q: "Can I go to sauna?"**
```javascript
if (inFertileWindow || possiblyPregnant) {
  return `
❌ Avoid sauna during TTC window + early pregnancy:
- High temp (>38.5°C) can affect egg quality
- Early embryos sensitive to heat
- ESPECIALLY avoid for male partner (sperm quality drops 50-70% for 2-3 months!)

Safe alternatives:
✅ Warm shower (<37°C)
✅ Normal exercise
  `;
}
```

**Q: "My temperature trend looks different from last cycle"**
```javascript
const comparison = compareCycles(currentCycle, previousCycles);
if (!comparison.similarPattern) {
  return `
You're right - this cycle's temperature pattern is different:

Previous cycles: Clear biphasic (low → high after ovulation)
Current cycle: ${comparison.currentPattern}

Possible reasons:
1. Ovulation timing varies (normal variation 2-3 days)
2. Post-pill adjustment (first 3-6 cycles)
3. Stress/sleep/exercise changes

Recommendation: ${comparison.recommendation}
  `;
}
```

---

## Testing & Validation

### Test Cases from Cycle 3

```javascript
describe('Cycle 3 Prediction', () => {
  it('should detect Day 10 temperature dip as pre-ovulation signal', () => {
    const temps = [-0.03, -0.03, +0.13, +0.04, -0.12, -0.12, -0.15, -0.11, +0.05, -0.31];
    const dip = detectTempDip(temps);
    expect(dip.detected).toBe(true);
    expect(dip.day).toBe(10);
    expect(dip.magnitude).toBeCloseTo(-0.31);
  });
  
  it('should not confuse environmental temp with hormonal signal', async () => {
    const sfWeather = { day10: 30.3, day11: 30.1 };  // Heat wave
    const bodyTemp = { day10: -0.31, day11: +0.09 };  // Lowest during heat wave
    
    const result = await analyzeEnvironmentalFactors('SF', sfWeather, bodyTemp);
    expect(result.hormonal).toBe(true);
    expect(result.environmental).toBe(false);
  });
  
  it('should predict ovulation Day 16 from Day 15 LH surge', () => {
    const lhData = [
      { day: 13, ratio: 0.3 },
      { day: 14, ratio: 0.5 },
      { day: 15, ratio: 0.95 }  // Surge!
    ];
    
    const prediction = predictOvulation(15, {}, lhData, {});
    expect(prediction.predictedDay).toBeCloseTo(16, 0.5);
    expect(prediction.confidence).toBeGreaterThan(0.9);
  });
});
```

---

## Documentation Updates

### Case Study: Cycle 3 Success Story

Add to README:

```markdown
## Real-World Success: Cycle 3 (March 2026)

**Challenge:** Temperature trend less clear than previous cycles

**How Fertility Tracker Helped:**
1. ✅ Detected Day 10 temperature dip (-0.31°C)
2. ✅ Ruled out environmental factors (SF heat wave correlation analysis)
3. ✅ Tracked LH progression over 5 days
4. ✅ Predicted ovulation Day 16 (confirmed by sustained LH surge)
5. ✅ Optimized TTC timing (Day 15 morning + Day 16 morning)

**User Feedback:**
> "This time you predicted my ovulation really well. I still had my LH strip with 2 obvious lines this morning"

**Outcome:** Perfect timing achieved despite less obvious temperature pattern
```

---

## Next Steps

1. **Implement new features in `index.js`**
2. **Add weather API integration** (Open-Meteo)
3. **Create LH strip image analyzer** (optional - OpenCV)
4. **Update documentation** with new examples
5. **Publish to npm** as v2.0
6. **Submit to EvoMap** with Cycle 3 case study
7. **Share on ClaHub** for other users

---

## Config Schema v2.0

```json
{
  "user": {
    "location": "San Francisco, CA",
    "timezone": "America/Los_Angeles"
  },
  "cycle": {
    "startDate": "2026-03-10",
    "historicalCycles": [
      { "start": "2026-01-07", "length": 34 },
      { "start": "2026-02-10", "length": 32 }
    ]
  },
  "oura": {
    "tokenPath": "~/.config/oura/token.txt"
  },
  "alerts": {
    "partner": "partner@example.com",
    "enableWeatherCorrelation": true,
    "enableLHImageAnalysis": false,
    "enableSpermViabilityCalc": true
  },
  "advanced": {
    "tempDipThreshold": -0.25,
    "hrvDropThreshold": 0.30,
    "lhSurgeThreshold": 0.85
  }
}
```

---

**Ready to implement?** Let me know which features to prioritize! 🥬
