<script>
  //@ts-nocheck
  import { Row, Col } from "svelte-materialify";
  import { navigate } from "svelte-navigator";
  export let num;
  export let arab;
  export let arti;
  export let nama;

  function openSurah() {
    localStorage.setItem("index", num);
    navigate("surah");
  }
</script>

<!-- svelte-ignore a11y-invalid-attribute -->
<div class="mb-3">
  <a href="#" on:click|preventDefault={openSurah}>
    <div
      class="quran-title elevation-3 rounded-lg pl-4 pr-4 pt-3 pb-3 hover-effect"
    >
      <Row class="ma-0 pa-0">
        <div class="number-circle">
          <span>{num}</span>
        </div>
      </Row>
      <Row class="ma-0 pa-0">
        <Col cols="12" md="6" class="pa-2">
          <h2 class="text-h5 mb-1 black-text font-weight-medium">
            {nama}
          </h2>
          <p class="subtitle mb-0">({arti})</p>
        </Col>
        <Col cols="12" md="6" class="pa-2 d-flex align-center justify-end">
          <p class="arab font-kitab-bold mb-0">
            {arab}
          </p>
        </Col>
      </Row>
    </div>
  </a>
</div>

<style>
  .quran-title {
    border-left-style: solid;
    border-left-color: #2e7d32;
    border-left-width: 6px;
    background-color: #ffffff;
    transition: all 0.3s ease;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }

  .hover-effect:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  }

  .number-circle {
    background-color: #2e7d32;
    color: white;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 600;
    margin: 0 0 8px 0;
  }

  .arab {
    font-size: clamp(20px, 3vw, 28px);
    color: #2e7d32;
    line-height: 1.4;
  }

  .subtitle {
    color: #666;
    font-size: 0.85rem;
  }

  a {
    text-decoration: none;
    color: inherit;
  }

  @media (max-width: 600px) {
    .quran-title {
      padding: 10px !important;
    }

    .arab {
      margin-top: 6px;
      font-size: 18px;
    }

    .number-circle {
      margin: 0 auto 6px auto;
      width: 25px;
      height: 25px;
    }
  }
</style>
