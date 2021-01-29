<template>
  <div class="container">
    <h3 class="text-center">Maroc</h3>
    <p>There have been approximately*</p>
    <div class="total-doses text-center my-2">
      <h2 class="total-vac">
        {{ !Total ? 0 : Total }} <span class="text-danger">vaccine doses</span>
      </h2>
    </div>
    <p>
      administered for COVID-19, currently at rate of about
      <strong class="text-dark">45.84/sec</strong> or
      <strong class="text-dark">3,960,339</strong> each day. That would be
      enough to give 1 dose to <strong class="text-dark">0.94%</strong> of the
      world's <br />
      population (~7.76 billion). At this rate, 70% of the population could be
      vaccinated (2 doses) in <strong class="text-dark">2,724 days</strong> (or
      by 11 Jul 2028). There are 58 countries that have started reporting
      vaccinations.
    </p>
    <div class="row py-2 ">
      <div class="col-xs-12 col-sm-6 col-md-4 mb-4">
        <div class="card text-center">
          <ul class="list-group list-group-flush">
            <li class="list-group-item font-weight-normal">
              Total Doses / per 100
            </li>
          </ul>
          <div class="card-footer bg-dark text-white">
            {{ !totalDoses ? 0 : totalDoses}} / {{!perThousand ? 0 : perThousand}}
          </div>
        </div>
      </div>
      <div class="col-xs-12 col-sm-6 col-md-4 mb-4">
        <div class="card text-center">
          <ul class="list-group list-group-flush">
            <li class="list-group-item font-weight-normal">Reported Doses</li>
          </ul>
          <div class="card-footer bg-dark text-white">
            {{ !totalReported ? 0 : totalReported}}
          </div>
        </div>
      </div>
      <div class="col-xs-12 col-sm-6 col-md-4 mb-4">
        <div class="card text-center">
          <ul class="list-group list-group-flush">
            <li class="list-group-item font-weight-normal">
              Daily Doses / 7 Day Change
            </li>
          </ul>
          <div class="card-footer bg-dark text-white">
            3,960,339 / <span class="text-success">+ 1,243,823</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props:['Total','totalReported','totalDoses','perThousand']
};
</script>
<style scoped>
h3 {
  font-size: 50px;
  margin: 30px 0;
}
.total-vac {
  font-size: 80px;
  text-align: center;
}
.total-vac span {
  font-size: 20px;
  font-style: italic;
}
p {
  font-size: 18px;
  font-style: italic;
  font-weight: 400px;
  letter-spacing: -0.6px;
  line-height: 1.7;
  color: #929292a1;
}
</style>
