<template>
    <div class="menu" style="margin-top: 30px">
        <HeaderMenu/>
    </div>
    <div class="image2">
        <img src="@/assets/image.jpg">
        <div class="text">LỊCH SỬ ĐẶT LỊCH</div>
    </div>
    <table>
        <thead>
            <tr>
                <th>Khách hàng</th>
                <th>Lịch khám</th>
                <th style="padding-left: 30px;">Bác sĩ</th>
                <th>Dịch vụ</th>
                <th>Giá dịch vụ</th>
                <th>Ngày đặt</th>
            </tr>
        </thead>
        <tbody>
            <tr v-if="searchOrder == null">
                <td>No Data</td>
            </tr>
            <tr v-for="search in searchOrder" :key="search.orderID">
                <td>{{ search.customerName }}</td>
                <td>{{ search.bookingTime }}</td>
                <td>{{ search.employeeName }}</td>
                <td>{{ search.serviceName }}</td>
                <td>{{ search.price }}</td>
                <td>{{ search.created_at }}</td>
            </tr>
           
        </tbody>
    </table>

    <div class="footer-container">
        <div class="footer-left">
            <div class="footer-logo">
                <a href="http://localhost:8081/">
                    <img src="@/assets/logo.png">
                </a>
            </div>
            <div class="footer-item">
                <a href="https://www.facebook.com/pkmatNgoiSao">
                    <img src="@/assets/facebook.png">
                </a>
                <a href="https://www.youtube.com/@PhongkhamMatNgoiSao">
                    <img src="@/assets/youtube.png">
                </a>
                <a href="https://zalo.me/1118479193975234403">
                    <img src="@/assets/zalo.png">
                </a>
            </div>
        </div>
        <div class="footer-right">
            <p style="font-size:22px ;color: #54595f; font-weight: bold;">Thông Tin Liên Hệ</p>
            <p style="font-weight: bold; color: #61ce70;">_____</p> <br>
            <div class="diachi" style="display: flex;">
                <img src="@/assets/dia_chi.png" style="margin-right: 20px;">
                <p>Số nhà 22 liền kề 6A C17 bộ công an, làng Việt Kiều Châu Âu, Mộ Lao, Hà Đông, Hà Nội</p>
            </div><br>
            <div class="phone" style="display: flex;">
                <img src="@/assets/phone.png" style="margin-right: 20px;">
                <p>098 7654 321</p>
            </div><br>
            <div class="www" style="display: flex;">
                <img src="@/assets/www.png" style="margin-right: 20px;">
                <p>http://localhost:8081/</p>
            </div><br>
            <div class="time" style="display: flex;">
                <img src="@/assets/time.png" style="margin-right: 20px;">
                <p>Time: 8.00 - 19.00h hàng ngày (Kể cả thứ 7 và Chủ nhật)</p>
            </div>
        </div>
    </div>
</template>
<script>
import HeaderMenu from './HeaderMenu.vue'
import axios from 'axios';
export default {
    components: {
        HeaderMenu,
    },
    data() {
        return{
            customerID:'',
            searchOrder: {},
        }

    },
    created() {
   
  },
  methods: {
    async getHistory(customerID) {
        console.log('customerID', customerID)
      try {
        const response = await axios.get(`http://127.0.0.1:8000/api/history/${customerID}`);
        this.searchOrder = response.data;
        console.log('response', response.data)
        console.log('search', this.searchOrder);
      } catch (error) {
        console.error('Error fetching employee data:', error);
      }
    }
  },
  mounted() 
  {
    this.customerID = window.localStorage.getItem('customerID')
    this.getHistory(this.customerID);
    console.log('mount',  this.customerID)
  }
}
</script>
<style>
.image2 {
    position: relative;
    display: inline-block;
    padding-top: 30px;
}

.image2 img {
    display: block;
    width: 100%;
    height: auto;
}

.image2::before {
    content: "";
    position: absolute;
    top: 20px;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(255, 255, 255, 0.5);
    pointer-events: none;
}

.image2 .text {
    position: absolute;
    top: 60%;
    left: 20%;
    transform: translate(-50%, -50%);
    color: black;
    padding: 10px 20px;
    border-radius: 5px;
    font-size: 30px;
    font-weight: bold;
}


/*------------------------HistoryBooking--------------------------*/
table{
    width: 800px;
    height: 200px;
    margin: 0 auto;
    margin-top: 20px;
    font-family: Arial, Helvetica, sans-serif;
    font-weight: 100;
    border-radius: 10px;
    border-collapse: collapse;
    overflow: hidden;
    box-shadow: 0 0 20px #0000001a;
}
th, 
td{
    background-color: #ffffff33;
    padding: 15px;
    color: #54595f;
}
th{
    text-align: left;
}
thead th{
    background-color: #838aa7;
}
tbody tr:hover{
    background-color: #ac4e4e4d;
}
tbody td{
    position: relative;
}
tbody td:hover::before{
    content: "";
    position: absolute;
    background-color: #ca121233;
    left: 0;
    right: 0;
    top: -9999px;
    bottom: -9999px;
    z-index: -1;
}


/*------------------------Footer--------------------------*/
.footer-container {
    display: flex;
    margin-top: 50px;
    height: 400px;
    background-color: #f6f7fa;
}

.footer-left {
    margin-left: 80px;
    margin-top: 100px;
    flex: 2;
}

.footer-right {
    padding-top: 15px;
    margin-top: 100px;
    margin-right: 80px;
    flex: 1;
}

.footer-logo img {
    margin-left: 35px;
    padding-bottom: 30px;
    flex: 0;
    width: 100px;
    height: auto;
}

.footer-item img {
    margin-left: 15px;
    width: 35px;
    height: 35px;
}


.footer-right p {
    justify-content: flex-start;
    text-align: left;
    font-family: "Montserrat", Arial, Helvetica, sans-serif;
    color: #54595f;
}

.footer-right img {
    width: 15px;
    height: 20px
}
</style>