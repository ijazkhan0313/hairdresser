<template>
  <div class="container-fluid px-1 px-md-4 py-5 mx-auto">
    <div class="row d-flex justify-content-center">
      <div class="col-12 col-md-11 col-lg-10 col-xl-9">
        <div class="card card0 border-0">
          <div class="row">
            <div class="col-12">
              <div class="card card00 m-2 border-0">
                <div class="row text-center justify-content-center px-3">
                  <p class="prev text-danger"><span class="fa fa-long-arrow-left"> Go Back</span></p id="back">
                  <h3 class="mt-4">Simple Registration</h3>
                </div>
                <div class="d-flex flex-md-row px-3 mt-4 flex-column-reverse">
                  <div class="col-md-6">
                    <div class="card1">
                      <ul id="progressbar" class="text-center">
                        <li class="active step0"></li>
                        <li class="step0"></li>
                        <li class="step0"></li>
                        <li class="step0"></li>
                      </ul>
                      <h6 class="mb-5">Enter your Email</h6>
                      <h6 class="mb-5">Set password</h6>
                      <h6 class="mb-5">Select your country</h6>
                    </div>
                  </div>
                  <div class="col-md-6">
                    <div class="card2 first-screen show ml-2">
                      <div class="row text-center px-3 mr-2">
                        <div class="mb-2 col-2"> <span class="fa fa-reddit social"></span> </div>
                        <div class="mb-2 col-2"> <span class="fa fa-facebook social"></span> </div>
                        <div class="mb-2 col-2"> <span class="fa fa-linkedin social"></span> </div>
                        <div class="mb-2 col-2"> <span class="fa fa-google-plus social"></span> </div>
                        <div class="mb-2 col-2"> <span class="fa fa-twitter social"></span> </div>
                        <div class="mb-2 col-2"> <span class="fa fa-dropbox social"></span> </div>
                      </div>
                      <div class="row px-3 mt-4">
                        <div class="form-group mt-1 mb-1"> <input type="text" id="email" class="form-control" required> <label class="ml-3 form-control-placeholder" for="email">Email</label> </div>
                        <div class="next-button text-center mt-1 ml-2"> <span class="fa fa-arrow-right"></span> </div>
                      </div>
                      <div class="row px-3 mt-1 mb-5">
                        <div class="custom-control custom-checkbox"> <input checked id="customCheck1" type="checkbox" class="custom-control-input"> <label for="customCheck1" class="custom-control-label">I want to receive promo emails</label> </div>
                      </div>
                    </div>
                    <div class="card2 ml-2">
                      <div class="row px-3 mt-3">
                        <div class="form-group mt-1 mb-1"> <input type="password" id="pwd" class="form-control" required> <label class="ml-3 form-control-placeholder" for="pwd">Password</label> </div>
                        <div class="next-button text-center mt-1 ml-2"> <span class="fa fa-arrow-right"></span> </div>
                      </div>
                      <div class="row mt-3 mb-5">
                        <div class="col-12">
                          <p class="mb-1">Password must contain</p>
                          <div class="row">
                            <div class="col-6"><span class="fa fa-circle text-danger"></span> lower case</div>
                            <div class="col-6"><span class="fa fa-circle text-danger"></span> numbers</div>
                          </div>
                          <div class="row">
                            <div class="col-6"><span class="fa fa-circle text-danger"></span> upper case</div>
                            <div class="col-6"><span class="fa fa-circle text-danger"></span> 8-16 characters</div>
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="card2 ml-2">
                      <div class="row px-3 mt-3">
                        <p class="mb-0 w-100">Select your Country</p>
                        <div class="form-group mt-3 mb-4">
                          <div class="select mb-3"> <select name="account" class="form-control custom-select">
                              <option>India</option>
                              <option>USA</option>
                              <option>Germany</option>
                              <option>Mexico</option>
                            </select> </div>
                        </div>
                        <div class="next-button text-center mt-3 ml-2"> <span class="fa fa-arrow-right"></span> </div>
                      </div>
                    </div>
                    <div class="card2 ml-2">
                      <div class="row px-3 mt-2 mb-4 text-center">
                        <h2 class="col-12 text-danger"><strong>Success !</strong></h2>
                        <div class="col-12 text-center"><img class="tick" src="https://i.imgur.com/WDI0da4.gif"></div>
                        <h6 class="col-12 mt-2"><i>...Enjoy COOKIES...</i></h6>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-12">
                <div class="row px-3">
                  <h2 class="text-muted get-bonus mt-4 mb-5">Get Bonus <span class="text-danger">666</span> cookies</h2> <img class="pic ml-auto mr-3" src="https://i.imgur.com/NFodZjZ.png">
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';

onMounted(() => {
  let currentFs, nextFs, previousFs;

  // No BACK button on first screen
  if (document.querySelector(".show").classList.contains("first-screen")) {
    document.querySelector(".prev").style.display = 'none';
  }

  // Next button
  document.querySelectorAll(".next-button").forEach(button => {
    button.addEventListener('click', function() {
      currentFs = this.closest('fieldset');
      nextFs = currentFs.nextElementSibling;

      document.querySelector(".prev").style.display = 'block';

      currentFs.classList.remove("show");
      nextFs.classList.add("show");

      const progressItems = document.querySelectorAll("#progressbar li");
      const index = Array.from(document.querySelectorAll(".card2")).indexOf(nextFs);
      progressItems.forEach((item, i) => {
        item.classList.toggle("active", i === index);
      });

      currentFs.style.display = 'none';
      currentFs.style.position = 'relative';
      nextFs.style.display = 'block';
    });
  });

  // Previous button
  document.querySelectorAll(".prev").forEach(button => {
    button.addEventListener('click', function() {
      currentFs = document.querySelector(".show");
      previousFs = currentFs.previousElementSibling;

      currentFs.classList.remove("show");
      previousFs.classList.add("show");

      document.querySelector(".prev").style.display = 'block';

      if (document.querySelector(".show").classList.contains("first-screen")) {
        document.querySelector(".prev").style.display = 'none';
      }

      const progressItems = document.querySelectorAll("#progressbar li");
      const index = Array.from(document.querySelectorAll(".card2")).indexOf(currentFs);
      progressItems.forEach((item, i) => {
        item.classList.toggle("active", i === index);
      });

      currentFs.style.display = 'none';
      currentFs.style.position = 'relative';
      previousFs.style.display = 'block';
    });
  });
});
</script>

<style  scoped>
body {
  color: #000;
  overflow-x: hidden;
  height: 100%;
  background-color: #F44336;
  background-repeat: no-repeat
}

.card0 {
  background-color: #F5F5F5;
  border-radius: 8px;
  z-index: 0
}

.card00 {
  z-index: 0
}

.card1 {
  margin-left: 140px;
  z-index: 0;
  border-right: 1px solid #F5F5F5
}

.card2 {
  display: none
}

.card2.show {
  display: block
}

.social {
  border-radius: 50%;
  background-color: #FFCDD2;
  color: #E53935;
  height: 47px;
  width: 47px;
  padding-top: 16px;
  cursor: pointer
}

input,
select {
  padding: 2px;
  border-radius: 0px;
  box-sizing: border-box;
  color: #9E9E9E;
  border: 1px solid #BDBDBD;
  font-size: 16px;
  letter-spacing: 1px;
  height: 50px !important
}

select {
  width: 100%;
  margin-bottom: 85px
}

input:focus,
select:focus {
  -moz-box-shadow: none !important;
  -webkit-box-shadow: none !important;
  box-shadow: none !important;
  border: 1px solid #E53935 !important;
  outline-width: 0 !important
}

.custom-checkbox .custom-control-input:checked~.custom-control-label::before {
  background-color: #E53935
}

.form-group {
  position: relative;
  margin-bottom: 1.5rem;
  width: 77%
}

.form-control-placeholder {
  position: absolute;
  top: 0px;
  padding: 12px 2px 0 2px;
  transition: all 300ms;
  opacity: 0.5
}

.form-control:focus+.form-control-placeholder,
.form-control:valid+.form-control-placeholder {
  font-size: 95%;
  top: 10px;
  transform: translate3d(0, -100%, 0);
  opacity: 1;
  background-color: #fff
}

.next-button {
  width: 18%;
  height: 50px;
  background-color: #BDBDBD;
  color: #fff;
  border-radius: 6px;
  padding: 10px;
  cursor: pointer
}

.next-button:hover {
  background-color: #E53935;
  color: #fff
}

.get-bonus {
  margin-left: 154px
}

.pic {
  width: 230px;
  height: 110px
}

#progressbar {
  position: absolute;
  left: 35px;
  overflow: hidden;
  color: #E53935
}

#progressbar li {
  list-style-type: none;
  font-size: 8px;
  font-weight: 400;
  margin-bottom: 36px
}

#progressbar li:nth-child(3) {
  margin-bottom: 88px
}

#progressbar .step0:before {
  content: "";
  color: #fff
}

#progressbar li:before {
  width: 30px;
  height: 30px;
  line-height: 30px;
  display: block;
  font-size: 20px;
  background: #fff;
  border: 2px solid #E53935;
  border-radius: 50%;
  margin: auto
}

#progressbar li:last-child:before {
  width: 40px;
  height: 40px
}

#progressbar li:after {
  content: '';
  width: 3px;
  height: 66px;
  background: #BDBDBD;
  position: absolute;
  left: 58px;
  top: 15px;
  z-index: -1
}

#progressbar li:last-child:after {
  top: 147px;
  height: 132px
}

#progressbar li:nth-child(3):after {
  top: 81px
}

#progressbar li:nth-child(2):after {
  top: 0px
}

#progressbar li:first-child:after {
  position: absolute;
  top: -81px
}

#progressbar li.active:after {
  background: #E53935
}

#progressbar li.active:before {
  background: #E53935;
  font-family: FontAwesome;
  content: "\f00c"
}

.tick {
  width: 100px;
  height: 100px
}

.prev {
  display: block;
  position: absolute;
  left: 40px;
  top: 20px;
  cursor: pointer
}

.prev:hover {
  color: #D50000 !important
}

@media screen and (max-width: 912px) {
  .card00 {
      padding-top: 30px
  }

  .card1 {
      border: none;
      margin-left: 50px
  }

  .card2 {
      border-bottom: 1px solid #F5F5F5;
      margin-bottom: 25px
  }

  .social {
      height: 30px;
      width: 30px;
      font-size: 15px;
      padding-top: 8px;
      margin-top: 7px
  }

  .get-bonus {
      margin-top: 40px !important;
      margin-left: 75px
  }

  #progressbar {
      left: -25px
  }
}
</style>