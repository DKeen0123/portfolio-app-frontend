<script>
  export let crypto;
  const amount = crypto.market_data.price_change_percentage_24h;
  let color;
  let arrowRotation;
  if (amount > 0) {
    color = "#4fa656";
    arrowRotation = 180;
  } else if (amount < 0) {
    color = "#ff3d2b";
    arrowRotation = 0;
  } else {
    color = "#333";
    arrowRotation = 270;
  }
</script>

<div class="header">
  <div>
    <img class="logo" src={crypto.image.small} alt={`${crypto.name}-logo`} />
  </div>
  <div class="info">
    <div class="name">
      <h1>{crypto.name}</h1>
      <h4 class="subtitle">{crypto.symbol}</h4>
    </div>
    <p class="amount">
      ${Math.round(crypto.market_data.current_price.usd * 100) / 100}
    </p>

    <div class="ticker-percentage">
      <svg
        version="1.1"
        id="arrow"
        style={`fill: ${color}; transform: rotate(${arrowRotation}deg)`}
        x="0px"
        y="0px"
        width="123.959px"
        height="123.958px"
        viewBox="0 0 123.959 123.958">
        <g>
          <path
            d="M117.979,28.017h-112c-5.3,0-8,6.4-4.2,10.2l56,56c2.3,2.3,6.1,2.3,8.401,0l56-56
            C125.979,34.417,123.279,28.017,117.979,28.017z" />
        </g>
      </svg>

      <p style={`color: ${color}`}>{Math.round(amount * 100) / 100}%</p>
    </div>
  </div>
</div>

<style>
  * {
    margin: 0;
  }

  #arrow {
    height: 12px;
    width: 12px;
    margin-right: 4px;
  }

  .ticker-percentage {
    display: flex;
    align-items: center;
  }

  .header {
    display: flex;
    background-color: #191919;
    color: white;
    margin-bottom: 24px;
    padding: 16px;
    border-radius: 8px;
  }

  .logo {
    margin-right: 8px;
  }

  .name {
    display: flex;
    align-items: baseline;
    margin-bottom: 8px;
  }

  .amount {
    font-size: 30px;
  }

  .subtitle {
    color: grey;
    margin-left: 4px;
  }
</style>
