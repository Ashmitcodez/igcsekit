<script lang="ts">
  import DataTable, { Head, Body, Row, Cell } from '@smui/data-table'

  import Comparison from '$lib/components/Comparison.svelte'
  import Callout from '$lib/components/Callout.svelte'

  let positives = [
    'Devices plugged into the computer are automatically detected and device drivers are automatically loaded up',
  ]

  let negatives = [
    'Maximum cable length is roughly 5 metres meaning it cannot be used over long distances',
  ]

  function calculateParityBit(parity: number, data: string): number {
    return (data.split('1').length - 1 + parity) % 2
  }

  let a: [string, string, string, string][] = []

  let parityBitData = [
    '0000000',
    '1111111',
    '0000001',
    '1010101',
  ]

  let parities = [0, 0, 1, 1]
  let parityNames = ['Even', 'Odd']

  for (let i = 0; i < parityBitData.length; i++) {
    const data = parityBitData[i]
    const parity = parities[i]
    const row: [string, string, string, string] = ['', '', '', '']
    const parityBit = calculateParityBit(parity, data).toString()
    row[0] = parityNames[parity]
    row[1] = data
    row[2] = parityBit
    row[3] = parityBit + data
    a.push(row)
  }
</script>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap" rel="stylesheet">
</svelte:head>

<section>
  <h1>Data Transmission</h1>
  <h2>Types and Methods</h2>
  <h3>Wired Connections</h3>
  <p>There are 2 ways data can be transmitted in terms of bits and wires.</p>
  <ul>
    <li>
      <strong>Serial</strong>: bits are transmitted <strong>one by one</strong> along a <strong>single wire</strong>
      <ul>
        <li>less likely to experience <strong>interference</strong> means data is less likely to have errors</li>
        <li>can be used for longer distances</li>
        <li>bits do not have to be reordered</li>
      </ul>
    </li>
    <li>
      <strong>Parallel</strong>: multiple bits are transmitted <strong>simultaneously</strong> across <strong>multiple wires</strong>
      <ul>
        <li>faster transmission than serial</li>
        <li>unlikely to skew when the connection is a short distance</li>
      </ul>
    </li>
  </ul>
  <p>Skewing occurs when bits travel at different speeds and arrive out of sync. This is only a problem with parallel data transmission.</p>
  <p>There are 3 methods that determine the direction of data transmission.</p>
  <ul>
    <li>
      <strong>Simplex</strong>: data transmission only occurs in one direction from the transmitter to the receiver
    </li>
    <li>
      <strong>Half-Duplex</strong>: data can be transmitted and received by both sides but both sides can't transmit data at the same time
    </li>
    <li>
      <strong>Full-Duplex</strong>: data transmission can occur in both directions simultaneously
    </li>
  </ul>
  <Callout emoji="🤔">
    Data transmission cables are a combination of (serial or parallel) and (simplex or half-duplex or full-duplex).
  </Callout>
  <h3>USB</h3>
  <p>The <strong>Universal Serial Bus</strong> is an <strong>asynchronous</strong> and <strong>serial</strong> method of transmitting data between devices and has become an industry standard.</p>
  <p>Using a USB is a common way of transmitting data from <strong>peripherals</strong> like keyboards, mice, and printers to personal computers. When a device is connected to a USB port, the computer <strong>automatically</strong>:</p>
  <ul>
    <li>detects that the device has been connected</li>
    <li>recognises the device and loads the appropriate <strong>device driver</strong> so that the device can communicate with the computer</li>
  </ul>
  <h4>Advantages and Disadvantages</h4>
  <Comparison {positives} {negatives}></Comparison>
  <h3>Data Packets</h3>
  <p>TCP stands for Transmission Control Protocol and allows programs and computers to exchange information over a network. Information is broken down into <strong>packets</strong> before transmission because smaller chunks of data are easier and quicker to route than large chunks of data.</p>
  <p>Data transmitted over the internet can include any media such as text, images, audio, video, markup, or a combination of theses.</p>
  <h4>Packet Structure</h4>
  <p>The information stored in a data packet is called the <strong>payload</strong>.</p>
  <p>Like any letter, email, or parcel, packets have 3 main components.</p>
  <ul>
    <li>From: <strong>Source IP Address</strong></li>
    <li>To: <strong>Destination IP Address</strong></li>
    <li>Content: <strong>Payload</strong></li>
  </ul>
  <p>Packets are split into 3 parts.</p>
  <ul>
    <li>Header</li>
    <li>Payload</li>
    <li>Trailer</li>
  </ul>
  <p>The header contains metadata about the packet and adds context to the payload.</p>
  <ul>
    <li><strong>Source IP</strong></li>
    <li><strong>Destination IP</strong></li>
    <li><strong>Packet Number</strong></li>
  </ul>
  <h4>Packet Switching</h4>
  <p>A router controls the route a data packet takes. Data packets usually take the most optimal route (path). Packets may arrive out of order or through different routes. This means the packets need to be reordered once the last packet arrives.</p>
  <ol>
    <li>Data is <strong>broken</strong> into packets</li>
    <li>A router controls the route a packet takes</li>
    <li>The fastest available route is selected</li>
    <li>Packets may arrive out of order</li>
    <li>Packets are <strong>reordered</strong> once the last packet has arrived</li>
    <li>Any missing or corrupted packets are requested to be resent</li>
  </ol>
  <p>Packet switching has many advantages.</p>
  <ul>
    <li>Interference and corruption are minimal since individual packets can be resent instead of the whole file</li>
    <li>Resending only corrupted packets can save time and <strong>bandwidth</strong> compared to resending an entire file</li>
  </ul>
  <h2>Error Detection</h2>
  <h3>Parity Check</h3>
  <p>Parity checks can come in 2 forms:</p>
  <ul>
    <li>parity bit</li>
    <li>parity byte</li>
  </ul>
  <p>The sender and receiver must agree on odd or even parity before transmission. A parity bit is added to the data to make sure that the number of <code>1</code> digits is even or odd</p>
  <DataTable>
    <Head>
      <Row>
        <Cell>Parity</Cell>
        <Cell>Data</Cell>
        <Cell>Parity Bit</Cell>
        <Cell>Final Value</Cell>
      </Row>
    </Head>
    <Body>
      {#each a as row}
        <Row>
          {#each row as cell,i}
            <Cell>
              {#if i}
                <code>{cell}</code>
              {:else}
                {cell}
              {/if}
            </Cell>
          {/each}
        </Row>
      {/each}
    </Body>
  </DataTable>
  <h3>Checksum</h3>
  <p>A checksum can determine whether data has been corrupted but it does not reveal where the error has been made. A checksum is calculated once by the sender and once by the receiver.</p>
  <ol>
    <li>Sender and receiver agree on checksum algorithm</li>
    <li>Sender calculates a value from the data</li>
    <li>Value is sent along with data</li>
    <li>Receiver recalculates value</li>
    <li>Error has occurred if both values are not equal</li>
    <li>Receiver requests for the data to be resent</li>
  </ol>
  <h3>Check Digit</h3>
  <p>Validates data on data entry.</p>
  <h3>ARQ</h3>
  <p>An automatic repeat request sends data in a loop until the sender receives a confirmation message. It does not <em>check</em> for errors and relies on other error checking methods to function effectively.</p>
  <ol>
    <li>Sender and receiver agree on a certain error checking method</li>
    <li>Sender transmits calculated value along with data</li>
    <li>Receiver checks or recalculates value</li>
    <li>Receiver sends acknowledgement if no errors have been found</li>
    <li>Receiver requests resend if an error is found</li>
    <li>Sender resends data until receiver sends an acknowledgement</li>
  </ol>
</section>