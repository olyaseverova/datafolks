<template>
  <div class="hello">
    <main class="main">
      <h1 class="size46 text-center text-uppercase my-5">
        Реализованные проекты
      </h1>
      <p class="text-center size18">
        Коммуникационное агентство – часть многофункционального холдинга,
        объединяющего различные компании на территории России и ближнего
        зарубежья.
      </p>
      <p class="text-center size18">
        Наши подходы к организации бизнеса и имеющиеся ресурсы позволяют
        одинаково эффективно обеспечивать реализацию как крупномасштабных
        федеральных или международных проектов, так и решать небольшие локальные
        задачи. Мы находимся в постоянном развитии, расширяя и укрепляя
        имеющиеся бизнес-направления, а также формируя новые.
      </p>
      <ul class="projects-list">
        <li
          class="projects-list__item"
          v-for="project in projects"
          :key="project.id"
          :id="project.id"
          :class="{ none: project.none }"
        >
          <img
            class="projects-list__img"
            :src="project.src"
            :alt="project.name"
          />
          <button
            type="button"
            class="projects-list__button text-uppercase"
            @click="showInfoProject"
            :id="project.id"
          >
            {{ project.name }}
          </button>
          <div class="projects-list__info none" :id="project.id">
            <p class="projects-list__text">{{ project.text }}</p>
            <button
              type="button"
              class="projects-list__hide text-uppercase download-button"
              @click="hideInfoProject"
              :id="project.id"
            >
              Скрыть
            </button>
          </div>
        </li>
      </ul>
      <button
        class="download-button text-uppercase"
        type="button"
        @click="showProjects"
      >
        Загрузить еще
      </button>
      <button
        class="download-button text-uppercase none hide_button"
        type="button"
        @click="hideProjects"
      >
        Скрыть
      </button>
    </main>
    <footer class="main-footer">
      <div class="contacts">
        <h1 class="size46 text-uppercase main-footer__headline">Контакты</h1>
        <p class="size18">Коммуникационное агентство</p>
        <p class="adress size18">
          344000, Россия, г. Ростов-на-Дону ул. Мира, д. 12 Бизнес–центр «Рост»,
          оф. 104
        </p>
        <div class="info">
          <ul class="contacts-list">
            <li
              class="contacts-list__item"
              v-for="contact in contacts"
              :key="contact.id"
            >
              <a
                class="contacts-list__phone no-underline"
                :href="contact.href"
                >{{ contact.number }}</a
              >
            </li>
          </ul>
          <div class="blue-block">
            <p class="blue-block__text size18">Email:</p>
            <a
              class="blue-block__text link no-underline size18"
              href="mailto:info@example.com"
              >info@example.com</a
            >
            <a
              href="https://www.facebook.com/"
              class="blue-block__text margin-45 link no-underline size18"
              >Facebook.com/exampleagency</a
            >
          </div>
        </div>
      </div>
      <form
        class="sign-up"
        method="post"
        action=""
        enctype="multipart/form-data"
      >
        <input
          class="sign-up__input"
          placeholder="Полное имя"
          type="text"
          id="name"
          required
        />
        <input
          class="sign-up__input"
          placeholder="E-mail"
          type="email"
          id="email"
          pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}$"
          size="30"
          required
        />
        <input
          class="sign-up__input"
          placeholder="Телефон"
          type="tel"
          id="tel"
          pattern="\+?[0-9\s\-\(\)]+"
          required
        />
        <textarea
          class="sign-up__textarea"
          placeholder="Пожалуйста, опишите задачу"
        ></textarea>
        <a href="#" class="sign-up__link blue-block__text link">
          Политика обработки персональных данных
        </a>
        <button class="sign-up__button text-uppercase" type="submit">
          Отправить заявку
        </button>
      </form>
    </footer>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  methods: {
    showProjects: function (event) {
      let showedProjectId = 0;
      let maxProjectId = 0;
      let hideButton = document.querySelector(".hide_button");
      let projectItems = document.querySelectorAll(".projects-list__item");
      projectItems.forEach(function (project) {
        if (!project.classList.contains("none")) {
          showedProjectId = project.id;
        }
        maxProjectId = project.id;
      });
      projectItems.forEach(function (project) {
        if (
          parseInt(project.id) === parseInt(showedProjectId) + 1 ||
          parseInt(project.id) === parseInt(showedProjectId) + 2 ||
          parseInt(project.id) === parseInt(showedProjectId) + 3
        ) {
          project.classList.remove("none");
        }
        if (
          parseInt(project.id) === parseInt(maxProjectId) &&
          !project.classList.contains("none")
        ) {
          event.target.classList.add("none");
          hideButton.classList.remove("none");
        }
      });
    },

    hideProjects: function (event) {
      let downloadButton = document.querySelector(".download-button");
      let projectItems = document.querySelectorAll(".projects-list__item");
      projectItems.forEach(function (project) {
        project.classList.add("none");
        if (parseInt(project.id) < 3) {
          project.classList.remove("none");
        }
      });
      event.target.classList.add("none");
      downloadButton.classList.remove("none");
    },

    showInfoProject: function (event) {
      let projectsInfo = document.querySelectorAll(".projects-list__info");
      projectsInfo.forEach(function (info) {
        if (info.id === event.target.id) {
          info.classList.remove("none");
        }
      });
    },

    hideInfoProject: function (event) {
      let projectsInfo = document.querySelectorAll(".projects-list__info");
      projectsInfo.forEach(function (info) {
        if (info.id === event.target.id) {
          info.classList.add("none");
        }
      });
    },
  },

  data() {
    return {
      projects: [
        {
          src: require("@/img/project1.png"),
          name: "Республика Саха",
          text: "Якутия, или Республика Саха – самый крупный по территории регион России и одна из самых крупных административных единиц в мире. Будь Якутия самостоятельным государством, она занимала бы 8-ое место в мире по площади. При этом по численности населения Саха остается одной из самой малозаселенных территорий. На 1 человека здесь приходится почти 3 кв. км. Это обуславливается тем, что почти 40 % земель региона расположены за Северным полярным кругом.",
          id: 0,
        },
        {
          src: require("@/img/project2.png"),
          name: "Газпром",
          text: "Публичное акционерное общество «Газпром» — российская транснациональная энергетическая компания, более 50 % акций которой принадлежит государству. Является холдинговой компанией Группы «Газпром». Непосредственно ПАО «Газпром» осуществляет только продажу природного газа и сдаёт в аренду свою газотранспортную систему.",
          id: 1,
        },
        {
          src: require("@/img/project3.png"),
          name: "Nokia",
          text: "Nokia Corporation (фин. Nokia Oyj, произносится но́киа) — финская транснациональная компания, производитель телекоммуникационного оборудования для мобильных, фиксированных, широкополосных и IP-сетей. В 2000-е годы доминировала на мировом рынке мобильных телефонов (с 2013 года телефоны под маркой Nokia выпускаются другими производителями).",
          id: 2,
        },
        {
          src: require("@/img/project5.png"),
          name: "МегаФон",
          text: "«МегаФон» — российская телекоммуникационная компания, предоставляющая услуги сотовой связи (GSM, UMTS, LTE и LTE Advanced), а также местной телефонной связи, широкополосного доступа в Интернет, кабельного телевидения и ряд сопутствующих услуг. Владеет виртуальным оператором сотовой связи «Yota», телекоммуникационной компанией «NetByNet» и онлайн-кинотеатром «START». Принадлежит холдингу USM[5][6].",
          none: true,
          id: 3,
        },
        {
          src: require("@/img/project4.png"),
          name: "Coca-Cola",
          text: "The Coca-Cola Company ([ðə ˈkoukə ˈkoulə ˈkʌmpənɪ], рус. компания «Кока-кола») — американская пищевая компания, крупнейший мировой производитель и поставщик концентратов, сиропов и безалкогольных напитков. Наиболее известным продуктом компании является напиток Coca-Cola. Входит в список Fortune 500 по итогам 2020 года (88-е место)[3]. Штаб-квартира находится в столице штата Джорджия, Атланте.",
          none: true,
          id: 4,
        },
        {
          src: require("@/img/project6.png"),
          name: "Volkswagen",
          text: "Volkswagen ([fɔlksˈvaːɡn], в переводе с нем. — «народный автомобиль») — немецкая автомобильная марка, одна из многих, принадлежащих концерну Volkswagen AG. Под этой маркой в 2019 году было реализовано 6 млн 620 тыс. автомобилей[источник не указан 581 день]. Штаб-квартира — в Вольфсбурге. Там же находится и Автомузей Volkswagen.",
          none: true,
          id: 5,
        },
        {
          src: require("@/img/project7.png"),
          name: "BMW",
          text: "BMW AG (рус. Бэ-Эм-Вэ́[2], аббревиатура от Bayerische Motoren Werke AG, с нем. — «Баварские моторные заводы») — немецкий производитель автомобилей, мотоциклов, двигателей, а также велосипедов. Председателем компании с 2006 по 2015 год был Норберт Райтхофер, с мая 2015 года — Харальд Крюгер, а с 18 июля 2019 года — Оливер Ципсе. Главный дизайнер — Йозеф Кабан[3]. Девиз компании — «Freude am Fahren», с нем. — «С удовольствием за рулём».",
          none: true,
          id: 6,
        },
        {
          src: require("@/img/project9.png"),
          name: "МТС",
          text: "МТС («Моби́льные ТелеСисте́мы») — российская компания, предоставляющая телекоммуникационные услуги, цифровые и медийные сервисы в России, Армении и Белоруссии под торговой маркой «МТС». Компания оказывает услуги сотовой связи (в стандартах GSM, UMTS (3G) , LTE и 5G), услуги проводной телефонной связи, мобильного и фиксированного, широкополосного доступа в Интернет, мобильного телевидения, кабельного телевидения, спутникового телевидения, цифрового телевидения, услуги по предоставлению медийного и развлекательного контента.",
          none: true,
          id: 7,
        },
        {
          src: require("@/img/project8.png"),
          name: "Mercedes-Benz",
          text: "Mercedes-Benz ([mɛʁˈtseːdəs ˈbɛnts] или [-dɛs-][2][3]; рус. Мерседе́с-Бенц[4]) — торговая марка и одноимённая компания — производитель легковых автомобилей премиального класса, грузовых автомобилей, автобусов и других транспортных средств, входящая в состав немецкого концерна «Daimler AG». Является одним из самых узнаваемых автомобильных брендов во всём мире[5]. Штаб-квартира Mercedes-Benz находится в Штутгарте, Баден-Вюртемберг, Германия.",
          none: true,
          id: 8,
        },
      ],

      contacts: [
        { number: "+7 (861) 300-11-28", href: "tel:+78613001128" },
        { number: "+7 (861) 300-11-52", href: "tel:+78613001152" },
        { number: "+7 (861) 300-11-52", href: "tel:+78613001152" },
      ],
    };
  },
};
</script>
