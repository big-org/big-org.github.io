---
layout: landing
permalink: '/new'
---

{% assign post = site.posts.first %}

{% assign d = post.meetupno %}
{% case d %}
  {% when '1' or '21' or '31' %}{% assign mettDate = d | append: "<sup>st</sup>" %}
  {% when '2' or '22' %}{% assign mettDate = d | append: "<sup>nd</sup>" %}
  {% when '3' or '23' %}{% assign mettDate = d | append: "<sup>rd</sup>" %}
  {% else %}{% assign mettDate = d | append: "<sup>th</sup>" %}
{% endcase %}
<section class="container">
  <div class="left-half half">
    <article>
      <div class="logo">
        <a href="/">
          <img src="/assets/big-org-small.png" alt="{{ site.title }}" />
        </a>
      </div>

      <h1>{{site.title}}</h1>
      <p>{{site.what}}</p>
      {% include menu.html %}
    </article>
  </div>
  <div class="right-half half">
    <article>
      <h3>{{mettDate}}</h3>
      <h4>{{post.title}}</h4>
      <!-- <div class="eventmeta">Thursday November 20 | EY, Trivandrum</div> -->
      <div class="eventmeta" id="clockdiv">
        <div>
          <span class="days"></span>
          <div class="smalltext">Days</div>
        </div>
        <div>
          <span class="hours"></span>
          <div class="smalltext">Hours</div>
        </div>
        <div>
          <span class="minutes"></span>
          <div class="smalltext">Minutes</div>
        </div>
        <div>
          <span class="seconds"></span>
          <div class="smalltext">Seconds</div>
        </div>
      </div>
    </article>
  </div>

</section>

<div class="section">
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quam culpa fuga, ducimus, modi suscipit nobis debitis a molestiae tempora sapiente natus veritatis cupiditate quo perferendis possimus. Dolore, ea! Voluptatibus, doloribus?
</div>

<script>
function getTimeRemaining(endtime) {
  var t = Date.parse(endtime) - Date.parse(new Date());
  var seconds = Math.floor((t / 1000) % 60);
  var minutes = Math.floor((t / 1000 / 60) % 60);
  var hours = Math.floor((t / (1000 * 60 * 60)) % 24);
  var days = Math.floor(t / (1000 * 60 * 60 * 24));
  return {
    'total': t,
    'days': days,
    'hours': hours,
    'minutes': minutes,
    'seconds': seconds
  };
}

function initializeClock(id, endtime) {
  var clock = document.getElementById(id);
  var daysSpan = clock.querySelector('.days');
  var hoursSpan = clock.querySelector('.hours');
  var minutesSpan = clock.querySelector('.minutes');
  var secondsSpan = clock.querySelector('.seconds');

  function updateClock() {
    var t = getTimeRemaining(endtime);

    daysSpan.innerHTML = t.days;
    hoursSpan.innerHTML = ('0' + t.hours).slice(-2);
    minutesSpan.innerHTML = ('0' + t.minutes).slice(-2);
    secondsSpan.innerHTML = ('0' + t.seconds).slice(-2);

    if (t.total <= 0) {
      clearInterval(timeinterval);
    }
  }

  updateClock();
  var timeinterval = setInterval(updateClock, 1000);
}
var deadline = new Date(Date.parse('{{post.start}}'));
var dateNow = new Date().getTime();
var diff = new Date('{{post.start}}').getTime() - dateNow;
if (diff > 0) {
  initializeClock('clockdiv', deadline);
} else {
  var clock = document.getElementById('clockdiv');
  clock.style.display = 'none';
}
</script>
