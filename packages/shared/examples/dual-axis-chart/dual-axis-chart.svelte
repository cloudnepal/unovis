<script lang='ts'>

  import { VisXYContainer, VisArea, VisAxis, VisLine } from '@unovis/svelte'
  import { XYDataRecord, generateXYDataRecords } from './data'

  const margin = { left: 100, right: 100, top: 40, bottom: 60 }
  const style: React.CSSProperties = { position: 'absolute', top: 0, left: 0, width: '100%', height: '40vh' }
  const chartX = d => d.x
  const chartAY = (d: XYDataRecord, i: number) => i * (d.y || 0)
  const chartBY = (d: XYDataRecord) => 20 + 10 * (d.y2 || 0)
  const xTicks = (x: number) => `${x}ms`
  const chartAYTicks = (y: number) => `${y}bps`
  const chartBYTicks = (y: number) => `${y}db`

</script>

<div>
  <VisXYContainer
    data={generateXYDataRecords(150)}
    autoMargin={false}
    margin={margin}
    width= {'100%'}
    height= {'40vh'}
  >
    <VisArea x={chartX} y={chartAY} opacity={0.9} />
    <VisAxis type='x' numTicks={3} tickFormat={xTicks} label='Time'/>
    <VisAxis type='y'
      tickFormat={chartAYTicks}
      tickTextWidth={60}
      tickTextColor={'#4D8CFD'}
      labelColor={'#4D8CFD'}
      label='Traffic'
    />
  </VisXYContainer>
  <VisXYContainer
    data={generateXYDataRecords(150)}
    yDomain={[0, 150]}
    margin={margin}
    autoMargin={false}
    width= {'100%'}
    height= {'40vh'}
    class={'chartContainer'}
  >
    <VisLine x={chartX} y={chartBY} color={'#FF6B7E'} />
    <VisAxis
      gridLine={false}
      tickTextColor={'#FF6B7E'}
      labelColor={'#FF6B7E'}
      label='Signal Strength'
    />
  </VisXYContainer>
</div>

<style>
  div :global(.chartContainer) {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 40vh;
  }
</style>
