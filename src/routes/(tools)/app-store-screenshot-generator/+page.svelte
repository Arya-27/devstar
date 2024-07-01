<style>
    .container1 {
      display: flex;
      justify-content:center;
      gap: 20px;
      padding: 20px;
      width: 100%;
      box-sizing: border-box;
      margin-left: 0px;
    }
  
    .column {
      flex: 1 1 auto;
      max-width: calc(20% - 10px);
      height: 350px;
      background-color: #f0f0f0;
      border: 1px solid #ccc;
      box-sizing: border-box;
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      align-items: center;
      text-align: center;
      padding: 20px;
      position: relative;
    }
  
    .column img {
      width: 100%;
      height: calc(100% - 50px);
      object-fit: cover;
      position: absolute;
      top: 100px;
      left: 0;
    }
  
    .column h2,
    .column p {
      margin: 0;
    }
  
    @media (max-width: 1200px) {
      .column {
        max-width: calc(25% - 20px);
      }
    }
  
    @media (max-width: 992px) {
      .column {
        max-width: calc(33.33% - 20px);
      }
    }
  
    @media (max-width: 768px) {
      .column {
        max-width: calc(50% - 20px);
      }
    }
  
    @media (max-width: 576px) {
      .column {
        max-width: 100%;
      }
    }
  </style>
  
  <div class="container1">
    <div class="column">
      <img src="https://th.bing.com/th/id/OIP.sxpCtMF39QV1bq9-0F4Y5QAAAA?w=355&h=488&rs=1&pid=ImgDetMain" alt="eImage 1">
      <h2>Column 1</h2>
      <p>This is the content of column 1.</p>
    </div>
    <div class="column">
      <img src="https://th.bing.com/th/id/OIP.sxpCtMF39QV1bq9-0F4Y5QAAAA?w=355&h=488&rs=1&pid=ImgDetMain" alt="eImage 1">
      <h2>Column 1</h2>
      <p>This is the content of column 1.</p>
    </div>
    <div class="column">
      <img src="https://th.bing.com/th/id/OIP.sxpCtMF39QV1bq9-0F4Y5QAAAA?w=355&h=488&rs=1&pid=ImgDetMain" alt="eImage 2">
      <h2>Column 2</h2>
      <p>This is the content of column 2.</p>
    </div>
    <div class="column">
      <img src="https://th.bing.com/th/id/OIP.sxpCtMF39QV1bq9-0F4Y5QAAAA?w=355&h=488&rs=1&pid=ImgDetMain" alt="eImage 3">
      <h2>Column 3</h2>
      <p>This is the content of column 3.</p>
    </div>
    <div class="column">
        <img src="https://th.bing.com/th/id/OIP.sxpCtMF39QV1bq9-0F4Y5QAAAA?w=355&h=488&rs=1&pid=ImgDetMain" alt="eImage 3">
        <h2>Column 3</h2>    
        <p>This is the content of column 3.</p>
      </div>
  </div>
  