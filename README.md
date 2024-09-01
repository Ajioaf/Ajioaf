<strategy>
  <meta>
    <name>RSI & MA Rise/Fall Bot</name>
    <description>Trades rise/fall options based on RSI and Moving Average crossover strategy.</description>
  </meta>
  
  <variables>
    <!-- Define variables -->
    <variable name="rsi_period" type="int" default="14"/>
    <variable name="ma_period" type="int" default="50"/>
    <variable name="rsi_upper_threshold" type="int" default="70"/>
    <variable name="rsi_lower_threshold" type="int" default="30"/>
    <variable name="trade_amount" type="float" default="1.0"/>
    <variable name="duration" type="int" default="5"/>
  </variables>
  
  <indicators>
    <!-- Define RSI and Moving Average indicators -->
    <indicator name="RSI" type="rsi">
      <period>${rsi_period}</period>
    </indicator>
    <indicator name="MA" type="moving_average">
      <period>${ma_period}</period>
    </indicator>
  </indicators>
  
  <logic>
    <!-- Logic for entering a rise trade -->
    <if>
      <condition type="and">
        <condition type="greater" left="RSI" right="${rsi_upper_threshold}"/>
        <condition type="greater" left="LastTick" right="MA"/>
      </condition>
      <then>
        <action type="trade">
          <symbol>R_100</symbol>
          <type>CALL</type>
          <amount>${trade_amount}</amount>
          <duration>${duration}</duration>
          <duration_unit>t</duration_unit>
        </action>
      </then>
    </if>
    
    <!-- Logic for entering a fall trade -->
    <if>
      <condition type="and">
        <condition type="less" left="RSI" right="${rsi_lower_threshold}"/>
        <condition type="less" left="LastTick" right="MA"/>
      </condition>
      <then>
        <action type="trade">
          <symbol>R_100</symbol>
          <type>PUT</type>
          <amount>${trade_amount}</amount>
          <duration>${duration}</duration>
          <duration_unit>t</duration_unit>
        </action>
      </then>
    </if>
  </logic>
</strategy>
