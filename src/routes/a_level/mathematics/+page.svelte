<script lang="ts">
  import LinkTree from '$lib/components/LinkTree.svelte'

  export let data
</script>

<section>
  <h1>Mathematics</h1>
  <LinkTree url={data.pathname} glob={import.meta.glob('./**/+page.svelte')}></LinkTree>
</section>

  <div id="notes">
    <h2>Completing the Square</h2>
    <p>The equation \(ax^2 + bx + c\) written in the form of \(y = a(x + b)^2 + c\) and \(y = (ax + b)^2 + c\) is called the complete square form.</p>

    <h3>Completing the Square Procedure:</h3>
    <ol>
      <li>Start with the quadratic expression \(ax^2 + bx + c\).</li>
      <li>Factor out the coefficient of \(x^2\).</li>
      <li>Complete the square by adding and subtracting \(\left(\frac{b}{2a}\right)^2\).</li>
      <li>Factor the perfect square trinomial.</li>
      <li>Simplify the expression.</li>
      <li>Express the result in the form \(y = a(x + b)^2 + c\).</li>
    </ol>

    <h3>Example:</h3>
    <p>Given \(ax^2 + bx + c\), express it in the form \(y = a(x + b)^2 + c\):</p>
    <p>\[ y = a\left(x + \frac{b}{2a}\right)^2 + \left(c - \frac{b^2}{4a}\right) \]
    </p>
    <h2>Completing the Square Example</h2>

      <p>Consider the quadratic expression \(4x^2 + 12x + 5\):</p>

      <p>
        \[ 4x^2 + 12x + 5 = 4(x^2 + 3x) + 5 \]<br>
        \[ = 4\left((x + \frac{3}{2})^2 - \left(\frac{3}{2}\right)^2\right) + 5 \]<br>
        \[ = 4((x + \frac{3}{2})^2 - \frac{9}{4}) + 5 \]<br>
        \[ = 4(x + \frac{3}{2})^2 - \9+5\]<br>
        \[ = 4(x + \frac{3}{2})^2 - \14\]
      </p>

      <h3>Vertex Form:</h3>
      <p>The vertex form allows easy identification of the vertex \((-b, c)\).</p>
      <p>Vertex: \(\left(-\frac{3}{2}, -\14\right)\)</p>
    </div>

    <h3>Additional Note:</h3>
    <p>If you want to express it in the form \(y = (ax + b)^2 + c\), you can factor out \(a\) from the perfect square trinomial.</p>
    <p>\[ y = \frac{(2ax + b)^2 + 4ac - b^2}{4a} \]</p>
</div>
