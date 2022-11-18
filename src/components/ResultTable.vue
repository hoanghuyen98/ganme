<template>
<section class="h-100 gradient-custom-2">
  <div class="container py-5 h-100">
    <div class="row d-flex justify-content-center align-items-center h-100">
      <div class="col">
        <div class="card">
            <div class="rounded-top text-white d-flex flex-row center-item" style="background-color: #000; height:200px;">
                <h1>KẾT QUẢ</h1>
            </div>

            <div class="card-body p-4 text-black">
                <table class="table align-middle mb-0 bg-white">
                    <thead class="bg-light">
                        <tr>
                            <th></th>
                            <th v-for="item in data" :key="item">{{item.name}}</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>
                                <div class="d-flex align-items-center">
                                    <p class="fw-bold mb-1">Trình Bày</p>
                                </div>
                            </td>
                            <td v-for="(item) in data" :key="item">
                                <p class="fw-normal mb-1">{{item.present_point}}</p>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <div class="d-flex align-items-center">
                                    <p class="fw-bold mb-1">Hỏi</p>
                                </div>
                            </td>
                            <td v-for="(item) in data" :key="item">
                                <p class="fw-normal mb-1 question-vote">{{item.question_point}}</p>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <div class="d-flex align-items-center">
                                    <p class="fw-bold mb-1">Đáp</p>
                                </div>
                            </td>
                            <td v-for="(item) in data" :key="item">
                                <p class="fw-normal mb-1 answer-vote">{{item.answer_point}}</p>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <div class="d-flex align-items-center">
                                    <p class="fw-bold mb-1">Cướp Điểm</p>
                                </div>
                            </td>
                            <td v-for="(item, index) in data" :key="item">
                                <p class="fw-normal mb-1" :data-id="index" @click="updateData($event)">???</p>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <div class="d-flex align-items-center">
                                    <p class="fw-bold mb-1">Tổng Điểm</p>
                                </div>
                            </td>
                            <td v-for="(item) in data" :key="item">
                                <p class="fw-normal mb-1 total-poin">{{item.total_1}}</p>
                            </td>
                        </tr>
                        <!-- <tr>
                            <td>
                                <div class="d-flex align-items-center">
                                    <p class="fw-bold mb-1">Tổng Điểm</p>
                                </div>
                            </td>
                            <td>
                                <p class="fw-normal mb-1" id='reduce'>10</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1 reduce">9</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">8</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">7</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">6</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">5</p>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <div class="d-flex align-items-center">
                                    <p class="fw-bold mb-1">Tổng Điểm</p>
                                </div>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">4</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">3</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">2</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">4</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">44</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">11</p>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <div class="d-flex align-items-center">
                                    <p class="fw-bold mb-1">Tổng Điểm</p>
                                </div>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">12</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">24</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">52</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">35</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1" @click="updateData($event)">???</p>
                            </td>
                            <td>
                                <p class="fw-normal mb-1">45</p>
                            </td>
                        </tr> -->
                    </tbody>
                </table>
            </div>
        </div>
      </div>
    </div>
  </div>
</section>
<div>
    <button @click="addClass">Add Class</button>
    <button @click="countTo(100, 50, 'reduce')">reduce</button>
    <button @click="countTo(0, 50, 'increase')">increase</button>
    <button @click="flyMeTo('reduce', 'increase', true)">di chuyen</button>
</div>
</template>
  
<script>
    import $ from "jquery";
    import { ref } from "vue";
    export default {

    setup() {
        const name_row = ['Trình Bày', 'Hỏi', 'Đáp', 'Cướp Điểm', 'Tổng Điểm']
        const id_team = ref(null)
        const data = [
            {
                "answer_point": 15, 
                "answer_vote": 0, 
                "id": 1, 
                "name": "Team 01", 
                "opposite_team": "Team 02", 
                "present_point": 85, 
                "question_point": 0, 
                "question_vote": 0,
                "total_1": 100,
                "total_2": 85,
            }, 
            {
                "answer_point": 0, 
                "answer_vote": 0, 
                "id": 2, 
                "name": "Team 02", 
                "opposite_team": "Team 01", 
                "present_point": 0, 
                "question_point": 16, 
                "question_vote": 2,
                "total_1": 16,
                "total_2": 31,
            },
            {
                "answer_point": 15, 
                "answer_vote": 2, 
                "id": 1, 
                "name": "Team 03", 
                "opposite_team": "Team 04", 
                "present_point": 85, 
                "question_point": 0, 
                "question_vote": 0,
                "total_1": 100,
                "total_2": 116,
            }, 
            {
                "answer_point": 0, 
                "answer_vote": 0, 
                "id": 2, 
                "name": "Team 04", 
                "opposite_team": "Team 03", 
                "present_point": 0, 
                "question_point": 16, 
                "question_vote": 0,
                "total_1": 16,
                "total_2": 0,
            },
            {
                "answer_point": 15, 
                "answer_vote": 2, 
                "id": 1, 
                "name": "Team 05", 
                "opposite_team": "Team 06", 
                "present_point": 0, 
                "question_point": 0, 
                "question_vote": 0,
                "total_1": 15,
                "total_2": 31,
            }, 
            {
                "answer_point": 0, 
                "answer_vote": 0, 
                "id": 2, 
                "name": "Team 06", 
                "opposite_team": "Team 05", 
                "present_point": 50, 
                "question_point": 16, 
                "question_vote": 0,
                "total_1": 66,
                "total_2": 50,
            },
        ]

        // const filterTeam = () => {
        //     return data.filter(
        //         item => 
        //     )
        // }

        const addClass = (index) => {
            for(let i = 0; i < data.length; i++){
                if(data[index]['name'] == data[i]['opposite_team']){
                    
                    if(data[index]['answer_vote'] > data[i]['question_vote']){
                        const answer_vote_element = document.getElementsByClassName('question-vote')[i]
                        answer_vote_element.setAttribute("id", "reduce");
                    }
                    else if(data[index]['question_vote'] > data[i]['answer_vote']){
                        const question_vote_element = document.getElementsByClassName('answer-vote')[i]
                        question_vote_element.setAttribute("id", "reduce");
                    }
                    //     const answer_vote_element = document.getElementsByClassName('answer-vote')[index]

                    // }
                    break
                } 
            }
        }
        
        const updateData = (event) => {
            const index = event.target.getAttribute("data-id")
           
          
            addClass(index)
            flyMeTo('reduce', event.target, true)
        }

        function flyMeTo(elem, destination, prepend) {
            var $elem = $('#' + elem);
            $elem.parent().append( "<p class='fw-normal mb-1'>0</p>" )
            
            var $dest = $(destination);
            const id_destination = $dest.attr('data-id')
            const total_point_element = document.getElementsByClassName('total-poin')[id_destination]
            // Early exit - if already in destination
            if($elem.parent().is(destination)) return;

            var $klon = $elem.clone().insertAfter($elem);
            let alam = document.getElementById(elem);
            if (alam) {
                var start = alam.getBoundingClientRect();
                $klon.css({position:"fixed", zIndex:9999, left:start.left, top:start.top, pointerEvents:'none'});
                $elem.css({opacity:0})[prepend?'prependTo':'appendTo']( $dest );

                var end = alam.getBoundingClientRect(); // Get new coordinates after append/prepend
                $klon.animate({left:end.left, top:end.top}, 1000, function() {
                    $klon.remove();         // Remove flying clone once it reaches destination
                    $elem.css({opacity:1}); // Show original Element
                    console.log('$elem: ', $elem.text())
                    $dest.text($elem.text());
                    console.log('$dest: ', $dest)
                    countTo(data[id_destination]['total_1'], data[id_destination]['total_2'], total_point_element)
                });
                $dest.text('???');
            }else {
                $dest.text('0')
                $dest.css({color:'red'});
                countTo(data[id_destination]['total_1'], data[id_destination]['total_2'], total_point_element)
            }

            
        }
        // DEMO:
        const eve1 = () => {
            console.log('>>>')
            flyMeTo( 'top', 'bottom', true ); // By passing `true` it will prepend!
        }
        const countTo = (from, to, total_point_element) => {
            let step = to > from ? 1 : -1;
            let interval = 50;
            if(from == to) {
                total_point_element.textContent = from
                // if(action == 'reduce') {
                //     document.querySelector(".reduce").textContent = from;
                // }
                // if (action == 'increase') {
                //     document.querySelector(".increase").textContent = from;
                // }
                return;
            }

            let counter = setInterval(function(){
                from += step;
                total_point_element.textContent = from
                // if(action == 'reduce') {
                //     document.querySelector('.reduce').textContent = from;
                // }
                // if (action == 'increase') {
                //     document.querySelector(".increase").textContent = from;
                // }
                if (from == to) {
                    clearInterval(counter);
                }
            }, interval);
        }

        return {
            data,
            name_row,
            updateData,
            countTo,
            flyMeTo,
            eve1,
            addClass,
            id_team,
        };
    },
    };
</script>
<style>
</style>
  