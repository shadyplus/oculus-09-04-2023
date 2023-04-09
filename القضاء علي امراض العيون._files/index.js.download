document.addEventListener("DOMContentLoaded", function () {
  // Вивід дати (+ час).
  postDate();
});

function postDate() {
  var body = document.body,
    postLang = body.getAttribute("data-post-lang");

  var sa = body.getAttribute("data-post-format") || "dd.mm.yyyy",
    msInDay = 86400000,
    counterLength = 90, // Максимальна кількість вімотаних днів. Змінюємо за необхідності.
    months,
    countryName = "ru",
    // Мова для місяців.
    isAbbreviated = body.getAttribute("data-post-abbreviated") ? true : false, // Скорочений варіант місяців до трьох букв
    localDate = new Date();

  var days = [
    "Воскресенье",
    "Понедельник",
    "Вторник",
    "Среда",
    "Четверг",
    "Пятница",
    "Суббота",
  ];

  switch (countryName) {
    case "ru": // Russia
    default:
      days = [
        "Воскресенье",
        "Понедельник",
        "Вторник",
        "Среда",
        "Четверг",
        "Пятница",
        "Суббота",
      ];
      break;
  }

  switch (countryName) {
    case "ru": // Русский
      months = [
        "Января",
        "Февраля",
        "Марта",
        "Апреля",
        "Мая",
        "Июня",
        "Июля",
        "Августа",
        "Сентября",
        "Октября",
        "Ноября",
        "Декабря",
      ];
      break;
  }
  if (isAbbreviated) {
    for (var i = 0; i < months.length; i++) {
      months[i] = months[i].slice(0, 3).toLowerCase(); // Прибираємо ".toLowerCase()", якщо перша буква повинна бути великою.
    }
  }

  for (var counter = 0; counter < counterLength; counter++) {
    var dateClass = "date-" + counter,
      nodeList = document.getElementsByClassName(dateClass),
      date = new Date(localDate.getTime() - counter * msInDay),
      timeCounter = 0,
      timeArray = time(nodeList /*, true*/); // Розкоментувати, якщо необхідне сортування в порядку спадання.

    timeArray = timeFormat(timeArray);

    for (var i = 0; i < nodeList.length; i++) {
      var data = nodeList[i].dataset;

      if (data.format) {
        nodeList[i].innerHTML = format(date, data.format);
        // format: особливий формать для окремої дати. Додаємo як data-format="фомарт".
        /// Формати дивитись в switch нижче. dd - числом, day - прописом.

        // Наприклад, <span class="date-1" data-format="dd month yyyy"></span>
        // мотає на 1 день назад і виводить цей span у вигляді "14 Лютого 2018".
      } else {
        // Загальний формат виводу дати змінювати ТУТ!
        nodeList[i].innerHTML = format(date, sa); // Default: dd.mm.yyyy
      }
      if (/\btime\b/.test(nodeList[i].className)) {
        nodeList[i].innerHTML += " " + timeArray[timeCounter]; // Рядок для формату виводу часу.
        timeCounter++;
      }
    }
  }

  for (var counter = 0; counter < counterLength; counter++) {
    var dateClass = "date" + counter,
      nodeList = document.getElementsByClassName(dateClass),
      date = new Date(localDate.getTime() + counter * msInDay),
      timeCounter = 0;

    for (var i = 0; i < nodeList.length; i++) {
      var data = nodeList[i].dataset;

      if (data.format) {
        nodeList[i].innerHTML = format(date, data.format);
      } else {
        nodeList[i].innerHTML = format(date, sa);
      }
    }
  }

  function time(nodeList, reverse) {
    var timeArray = [],
      timeStatement = false;

    for (var i = 0; i < nodeList.length; i++) {
      if (nodeList[i].className.match(/\btime\b/)) {
        if (nodeList[i].className.match(/\bdate-0\b/)) {
          timeStatement = true;
        }
        timeArray.push(timeRandom(timeStatement));
      }
    }

    if (reverse)
      timeArray.sort(function (a, b) {
        return b - a;
      });
    else
      timeArray.sort(function (a, b) {
        return a - b;
      });

    return timeArray;
  }

  function timeRandom(statement) {
    if (statement) {
      var date = new Date(),
        timeLimit = date.getHours() * 60 + date.getMinutes();

      return Math.round(0 + Math.random() * timeLimit);
    }
    return Math.round(0 + Math.random() * 1440);
  }

  function timeFormat(timearray) {
    var array = [];

    for (var i = 0; i < timearray.length; i++) {
      var htemp = Math.floor(timearray[i] / 60),
        mtemp = timearray[i] % 60,
        hours = htemp < 10 ? "0" + htemp : htemp,
        minutes = mtemp < 10 ? "0" + mtemp : mtemp;
      array.push(hours + ":" + minutes);
    }

    return array;
  }

  function notLastIteration(index, array) {
    return index !== array.length - 1;
  }

  function format(date, format) {
    var testFormat = ["dd", "day", "mm", "month", "yyyy", "year"];
    var innerDate = format;

    var dd = date.getDate(),
      mm = date.getMonth() + 1,
      year = date.getFullYear(),
      month = months[mm - 1],
      day = days[new Date(year, mm - 1, dd).getDay()];

    dd = dd < 10 ? "0" + dd : dd;
    mm = mm < 10 ? "0" + mm : mm;

    var dateFormat = {
      day: day,
      dd: dd,
      year: year,
      yyyy: year,
      mm: mm,
      month: month,
    };

    for (var i = 0; i < testFormat.length; i++) {
      var string = testFormat[i];
      var regExp = new RegExp(string);
      innerDate = innerDate.replace(regExp, dateFormat[string]);
    }

    return innerDate;
  }
}
// $(document).on('click', 'a[href^="#"]', function (event) {
//     event.preventDefault();
//     if (!$(this).hasClass('ignor')) $("html,body").animate({scrollTop: $(".card-form").offset().top - ($(window).height() - $(".card-form").outerHeight(true))}, 1e3);
// });
initializeTimer();
function initializeTimer() {
  if (!localStorage.getItem("ever-timer")) {
    var time = {
      hours: 0,
      minutes: 10,
      seconds: 0,
    };

    time = time.hours * 3600 + time.minutes * 60 + time.seconds;

    localStorage.setItem("time", time);
    localStorage.setItem("ever-timer", true);
  }

  // timerSettings();
}

function filling(obj, value) {
  for (var i = 0; i < obj.length; i++) {
    obj[i].innerHTML = value;
  }
}

function diFilling(obj, value) {
  for (var i = 0; i < obj.length; i++) {
    obj[i].innerHTML = value[i % 2];
  }
}

var time = 600;
var intr;
function start_timer() {
  intr = setInterval(tick, 1000);
}
function tick() {
  time = time - 1;
  var c = Math.floor(time / 60);
  var d = time - c * 60;
  if (c == 0 && d == 0) {
    clearInterval(intr);
  }
  d = d >= 10 ? d : "0" + d;
  $("#min").html("0" + c);
  $("#sec").html(d);
}
tick();
