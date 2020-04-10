<template>
  <div id="app">
    <div class="container">
      <header>
        <div class="header__personal">

          <div class="header__personal_item item1">
            <img src="./assets/avatar.png" alt="avatar" class="avatar">
          </div>

          <div class="header__personal_item item2">
            <h2 class="name">Вероника Ростова</h2>
            <p class="role">Менеджер по продажам</p>
            <div class="bio">
              <span class="longWordBreak">Подберу для вас самые лучшие предложения. Мои услуги абсолютно бесплатны.</span>
            </div>
          </div>

          <div class="header__personal_item item3">
            <table class="services">
              <thead>
                <tr>
                  <th></th>
                  <th>Услуги</th>
                </tr>
              </thead>
              <tfoot>
                <tr>
                  <td>Всего</td>
                  <td>15</td>
                </tr>
              </tfoot>
              <tbody>
                <tr  class="spaceUnder">
                  <td class="first_item">Ручное бронирование</td>
                  <td>11</td>
                </tr>
                <tr>
                  <td class="second_item">Пакетные туры</td>
                  <td>3</td>
                </tr>
                <tr class="spaceBelow">
                  <td class="third_item">Отели</td>
                  <td>1</td>
                </tr>
              </tbody>
            </table>
          </div>

        </div>
      </header>
      <main>
        <div class="main__info">
          <div class="main__info_item1">
            <span>Последние отзывы</span>
            <span><a href="#">Все отзывы</a></span>
          </div>
          <div class="main__info_item2">
            <span>131</span>
            <span>14</span>
          </div>
        </div>
        <transition-group name="fade">
          <div class="main__feedback" v-for="(item, i) in feedbacks" :key="i">
            <p class="feedback_owner">
              {{ item.name }}  <span class="date">{{ item.date }}</span>
            </p>
            <div class="feedback_message">
              <span class="longWordBreak">{{ item.message }}</span>
            </div>
          </div>
        </transition-group>
      </main>
    </div>

    <div class="container container_second_part">
      <footer>

        <textarea v-model="currentMessage" ref="mesaggeInput" @keydown.meta.enter="addMessage" @keydown.ctrl.enter="addMessage"></textarea>
        <div class="btn" @click="addMessage">Написать консультанту</div>

      </footer>
    </div>

  </div>
</template>

<script>



export default {
  name: 'App',
  data () {
    return {
      feedbacks: [
        {
          name: 'Cамуил',
          date: '13 октября 2011',
          message: 'Привет, Верунь! ниче себе ты крутая. фотка класс!!!! '
        },
        {
          name: 'Лилия Семёновна',
          date: '14 октября 2011',
          message: 'Вероника, здравствуйте! Есть такой вопрос: Особый вид куниц жизненно стабилизирует кинетический момент, это и есть всемирно известный центр огранки алмазов и торговли бриллиантами?'
        },
        {
          name: 'Лилия Семёновна',
          date: '14 октября 2011',
          message: 'Вероника, здравствуйте! Есть такой вопрос: Особый вид куниц жизненно стабилизирует кинетический момент?'
        }
      ],
      currentMessage: ''
    }
  },
  methods: {
    addMessage () {
      if (this.currentMessage.length) {
        const newMsg = {
          name: 'Лилия Семёновна',
          date: '14 октября 2011',
          message: this.currentMessage
        }
        this.feedbacks.push(newMsg)
        this.currentMessage = ''
        this.$refs.mesaggeInput.style.border = '1px solid #000000'
      } else {
        this.$refs.mesaggeInput.style.border = '1px solid red'
      }
    },
    loginfo () {
      console.log('lol')
    }
  }

}
</script>

<style>
  .fade-enter-active, .fade-leave-active {
    transition: opacity 1s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
    opacity: 0;
  }

  #app {
    background: #E5E5E5;
    font-family: Arial;
    font-style: normal;
    font-weight: normal;
    line-height: 19px;
  }

  .container {
    max-width: 680px;
    margin: 0 auto;
    background: white;
    padding: 15px 20px 25px 20px;
  }

  /*Header start*/

  .header__personal {
    display: grid;
    grid-template-columns: repeat(6, 1fr);

  }

  .item1 { grid-area: 1 / 1 / 2 / 2; }
  .item2 { grid-area: 1 / 2 / 2 / 7; }
  .item3 { grid-area: 2 / 2 / 6 / 7; }


  .avatar {
    border-radius: 50%;
    position: relative;
    z-index: 10;
  }

  .name, .role {
    margin-left: 10px;
  }

  .name {
    font-weight: bold;
    font-size: 16px;
    line-height: 20px;
    margin-bottom: 3px;
    margin-top: 5px;
  }

  .role {
    font-size: 12px;
    line-height: 20px;
    color: #808080;
    font-weight: normal;
    margin-bottom: 3px;
  }

  .bio {
    max-width: 100%;
    font-size: 14px;
    line-height: 20px;
    background: #FFFBC8;
    border: 1px solid #DADADA;
    border-radius: 5px;
    padding: 10px 5px 10px 40px;
    font-style: normal;
    font-weight: normal;
    color: #333333;
    margin-left: -30px;
    max-height: 42px;
    overflow-y: auto;
  }

  .longWordBreak {
    word-break: break-word;
  }

  table.services {
    width: 100%;
    margin-top: -2px;
    margin-bottom: 20px;
    border-collapse: separate;
  }

  table.services td:nth-child(even) {
    text-align: center;
  }


  table.services thead th {
    border-bottom: 1px solid #DADADA;
    font-size: 13px;
    line-height: 15px;
    padding-bottom: 10px;
  }

  table.services tfoot td {
    border-top: 1px solid #DADADA;
    padding-top: 10px;
    font-weight: bold;
    font-size: 16px;
    line-height: 26px;
  }

  table.services tbody tr.spaceUnder td {
    border-top: 15px solid white;
  }

  table.services tbody tr td:first-child {
    position: relative;
    z-index: 6;
    border-left: 1px solid #dadada;
    font-size: 13px;
    line-height: 26px;
  }

  table.services tbody tr.spaceBelow td {
    border-bottom: 15px solid white;
  }

  table.services thead tr th:first-child, table.services tfoot tr td:first-child {
    position: relative;
  }

  table.services tbody tr td:last-child {
    font-weight: bold;
    font-size: 13px;
    line-height: 15px;
  }

  table.services thead tr th:first-child:before {
    content: '';
    height: 17px;
    width: 4px;
    background: #ffffff;
    position: absolute;
    left: -2px;
    bottom: -18px;
    z-index: 20;
  }

  table.services tfoot tr td:first-child:before {
    content: '';
    height: 17px;
    width: 4px;
    background: #ffffff;
    position: absolute;
    z-index: 20;
    left: -2px;
    top: -19px;
  }

  table.services td {
    padding: 4px;
  }

  table.services tbody tr td:first-child:before {
    content: '';
    display: block;
    position: absolute;
    height: 20px;
    border-radius: 0px 3px 3px 0px;
    z-index: -1;
    padding: 0.3em;
    top: 2px;
    left: 0;
  }

  table.services tbody tr td.first_item:before {
    width: 73.3%;
    background: rgba(135, 225, 125, 0.6);
  }

  table.services tbody tr td.second_item:before {
    width: 20%;
    background: rgba(148, 208, 248, 0.6);
  }

  table.services tbody tr td.third_item:before {
    width: 6.6%;
    background: rgba(148, 208, 248, 0.6);
  }

  /*Header End*/

  /*Main start*/

  .main__info {
    display: flex;
    justify-content: space-between;
  }

  .main__info_item1 span:first-child {
    color: #333333;
    font-weight: bold;
    font-size: 16px;
    line-height: 16px;
    margin-right: 20px;
  }

  .main__info_item1 span:last-child a{
    color: #005DA1;
    font-size: 14px;
  }

  .main__info_item2 span:last-child {
    margin-left: 25px;
  }

  .main__info_item2 span {
    position: relative;
    padding-left: 15px;
    font-size: 12px;
    line-height: 14px;
  }

  .main__info_item2 span:before {
    content: '';
    display: block;
    width: 13px;
    height: 12px;
    position: absolute;
    left: 0;
    top: 1px;
  }

  .main__info_item2 span:first-child:before {
    background: url("./assets/like.png") no-repeat;
  }

  .main__info_item2 span:last-child:before {
    background: url("./assets/comment.png") no-repeat;
  }

  .main__feedback {
    margin-top: 20px;
  }

  .main__feedback .feedback_owner {
    font-weight: bold;
    font-size: 14px;
    line-height: 19px;
  }

  .main__feedback .feedback_owner .date{
    font-weight: normal;
    font-size: 14px;
    line-height: 20px;
    color: #808080;
  }

  .main__feedback .feedback_message {
    position: relative;
    background: #F2FBFF;
    border: 1px solid #C4CBCF;
    box-shadow: 0px 4px 10px rgba(128, 128, 128, 0.1);
    padding: 20px;
    font-size: 14px;
    line-height: 19px;
    margin-top: 15px;
  }

  .main__feedback .feedback_message:before, .main__feedback .feedback_message:after {
    content: '';
    position: absolute;
    display: inline-block;
    width: 0;
    height: 0;
    border-style: solid;
  }

  .main__feedback .feedback_message:before {
    border-color: transparent transparent transparent #C4CBCF;
    border-width: 15px 0 0 15px;
    top: -15px;
  }

  .main__feedback .feedback_message:after {
    border-color: transparent transparent transparent #F2FBFF;
    border-width: 13px 0 0 13px;
    left: 21px;
    top: -13px;

  }

  /*Main End*/


  /*Footer start*/

  .container_second_part {
    background: #F2F2F2;
  }

  footer textarea {
    resize: none !important;
    display: block;
    width: 100%;
    box-sizing: border-box;
    height: 63px;
    margin-top: 20px;
    border: 1px solid #000000;
    border-radius: 2px;
  }

  .btn {
    width: 50%;
    margin: 30px auto;
    background: #FDD639;
    border-radius: 23px;
    padding: 15px 0;
    text-align: center;
    font-weight: bold;
    font-size: 16px;
    line-height: 21px;
    -moz-user-select: none;
    -webkit-user-select: none;
    -ms-user-select:none;
    user-select:none;
    -o-user-select:none;
    cursor: pointer;
  }

  /*Footer end*/

  @media all and (max-width: 500px) {

    /*Header start*/

    header.container_first_part {
      padding-top: 5px;
    }

    .bio {
      font-size: 12px;
      line-height: 15px;
    }

    .item3 { grid-area: 2 / 1 / 3 / 7; }

    /*header end*/

    /*Main start*/

    .main__info_item1 span:first-child {
      font-size: 14px;
      margin-right: 10px;
    }

    .main__info_item1 span:last-child a {
      font-size: 12px;
    }

    .main__info_item2 span:last-child {
      margin-left: 10px;
    }

    /*Main end*/

    /*Footer start*/

    .btn {
      font-size: 12px;
    }

    /*Footer end*/

  }

</style>
