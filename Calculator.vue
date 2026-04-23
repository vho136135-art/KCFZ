<template>
  <div class="radar-calculator">
    <h2>Radar Equation Calculator</h2>
    <div class="form-container">
      <!-- Calculation Type -->
      <div class="form-group row">
        <label class="label" for="calculationType">Calculation Type:</label>
        <div class="input-with-dropdown">
          <select v-model="calculationType" id="calculationType" class="full-width">
            <option value="targetRange">Target Range</option>
            <!-- 可根据需要添加其他计算类型选项 -->
          </select>
        </div>
      </div>

      <!-- Radar Specifications -->
      <div class="form-group">
        <h3>Radar Specifications</h3>
        <div class="input-group">
          <label class="label" for="wavelength">Wavelength:</label>
          <div class="input-with-unit">
            <div class="input-wrapper">
              <input type="text" v-model="wavelength" id="wavelength" class="full-width">
            </div>
            <div class="unit-wrapper">
              <select v-model="wavelengthUnit" class="unit-select">
                <option value="m">m</option>
                <!-- 可添加其他单位选项 -->
              </select>
            </div>
          </div>
        </div>
        <div class="input-group">
          <label class="label" for="pulseWidth">Pulse Width:</label>
          <div class="input-with-unit">
            <div class="input-wrapper">
              <input type="text" v-model="pulseWidth" id="pulseWidth" class="full-width">
            </div>
            <div class="unit-wrapper">
              <select v-model="pulseWidthUnit" class="unit-select">
                <option value="μs">μs</option>
                <!-- 可添加其他单位选项 -->
              </select>
            </div>
          </div>
        </div>
        <div class="input-group">
          <label class="label" for="systemLosses">System Losses:</label>
          <div class="input-with-unit">
            <div class="input-wrapper">
              <input type="text" v-model="systemLosses" id="systemLosses" class="full-width">
            </div>
            <div class="unit-wrapper">
              <select v-model="systemLossesUnit" class="unit-select">
                <option value="dB">dB</option>
                <!-- 可添加其他单位选项 -->
              </select>
            </div>
          </div>
        </div>
        <div class="input-group">
          <label class="label" for="noiseTemperature">Noise Temperature:</label>
          <div class="input-with-unit">
            <div class="input-wrapper">
              <input type="text" v-model="noiseTemperature" id="noiseTemperature" class="full-width">
            </div>
            <div class="unit-wrapper">
              <select v-model="noiseTemperatureUnit" class="unit-select">
                <option value="K">K</option>
                <!-- 可添加其他单位选项 -->
              </select>
            </div>
          </div>
        </div>
        <div class="input-group">
          <label class="label" for="targetRadarCrossSection">Target Radar Cross Section:</label>
          <div class="input-with-unit">
            <div class="input-wrapper">
              <input type="text" v-model="targetRadarCrossSection" id="targetRadarCrossSection" class="full-width">
            </div>
            <div class="unit-wrapper">
              <select v-model="targetRadarCrossSectionUnit" class="unit-select">
                <option value="m²">m²</option>
                <!-- 可添加其他单位选项 -->
              </select>
            </div>
          </div>
        </div>
        <div class="input-group">
          <label class="label" for="configuration">Configuration:</label>
          <div class="input-with-dropdown">
            <div class="input-wrapper">
              <select v-model="configuration" id="configuration" class="full-width">
                <option value="monostatic">Monostatic</option>
                <!-- 可根据需要添加其他配置选项 -->
              </select>
            </div>
          </div>
        </div>
        <div class="input-group">
          <label class="label" for="gain">Gain:</label>
          <div class="input-with-unit">
            <div class="input-wrapper">
              <input type="text" v-model="gain" id="gain" class="full-width">
            </div>
            <div class="unit-wrapper">
              <select v-model="gainUnit" class="unit-select">
                <option value="dB">dB</option>
                <!-- 可添加其他单位选项 -->
              </select>
            </div>
          </div>
        </div>
      </div>

      <!-- Transmit Power and SNR -->
      <div class="form-group">
        <h3>Transmit Power and SNR</h3>
        <div class="input-group">
          <label class="label" for="peakTransmitPower">Peak Transmit Power:</label>
          <div class="input-with-unit">
            <div class="input-wrapper">
              <input type="text" v-model="peakTransmitPower" id="peakTransmitPower" class="full-width">
            </div>
            <div class="unit-wrapper">
              <select v-model="peakTransmitPowerUnit" class="unit-select">
                <option value="kW">kW</option>
                <!-- 可添加其他单位选项 -->
              </select>
            </div>
          </div>
        </div>
        <div class="input-group">
          <label class="label" for="snr">SNR:</label>
          <div class="input-with-unit">
            <div class="input-wrapper">
              <input type="text" v-model="snr" id="snr" class="full-width">
            </div>
            <div class="unit-wrapper">
              <select v-model="snrUnit" class="unit-select">
                <option value="dB">dB</option>
                <!-- 可添加其他单位选项 -->
              </select>
            </div>
          </div>
        </div>
      </div>

      <!-- Result -->
      <div class="form-group">
        <h3>Result</h3>
        <div class="input-group">
          <label class="label" for="targetRange">Target Range:</label>
          <div class="input-with-unit">
            <div class="input-wrapper">
              <input type="text" v-model="targetRange" id="targetRange" readonly class="full-width">
            </div>
            <div class="unit-wrapper">
              <select v-model="targetRangeUnit" class="unit-select">
                <option value="km">km</option>
                <!-- 可添加其他单位选项 -->
              </select>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Calculator',
  data() {
    return {
      calculationType: 'targetRange',
      wavelength: '0.3',
      wavelengthUnit: 'm',
      pulseWidth: '1',
      pulseWidthUnit: 'μs',
      systemLosses: '0',
      systemLossesUnit: 'dB',
      noiseTemperature: '290',
      noiseTemperatureUnit: 'K',
      targetRadarCrossSection: '1',
      targetRadarCrossSectionUnit: 'm²',
      configuration: 'monostatic',
      gain: '20',
      gainUnit: 'dB',
      peakTransmitPower: '1',
      peakTransmitPowerUnit: 'kW',
      snr: '10',
      snrUnit: 'dB',
      targetRange: '10.32',
      targetRangeUnit: 'km'
    };
  }
};
</script>

<style scoped>
.radar-calculator {
  padding: 20px;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  width: 400px;
  margin: 0 auto;
}

.form-container {
  padding: 10px;
}

.form-group {
  margin-bottom: 15px;
  border-bottom: 1px solid #ccc;
  padding-bottom: 10px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.form-group.row {
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.input-group {
  display: flex;
  align-items: center;
  width: 100%;
  margin-bottom: 5px;
}

.label {
  min-width: 150px;
  text-align: left;
  margin-right: 10px;
  flex: 1;
}

.full-width {
  width: 100%;
}

.unit-select {
  width: 60px; /* 保持单位选择器宽度较小 */
}

.input-with-unit,
.input-with-dropdown {
  display: flex;
  align-items: center;
}

.input-wrapper {
  margin-right: 5px;
}

.unit-wrapper {
  margin-left: 5px;
}
</style>