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
                                <p class="fw-normal mb-1">{{item.point.present}}</p>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <div class="d-flex align-items-center">
                                    <p class="fw-bold mb-1">Hỏi</p>
                                </div>
                            </td>
                            <td v-for="(item) in data" :key="item">
                                <p class="fw-normal mb-1 question-vote">{{item.point.question}}</p>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <div class="d-flex align-items-center">
                                    <p class="fw-bold mb-1">Đáp</p>
                                </div>
                            </td>
                            <td v-for="(item) in data" :key="item">
                                <p class="fw-normal mb-1 answer-vote">{{item.point.answer}}</p>
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
                                <p class="mb-1 total-point">{{item.point.total}}</p>
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
    import ApiService from "@/services/api.service";
    import { ref } from "vue";
    export default {

    setup() {
        const name_row = ['Trình Bày', 'Hỏi', 'Đáp', 'Cướp Điểm', 'Tổng Điểm']
        const data_default = ApiService.getData()
        console.log('data_default: ', data_default)
        const id_team = ref(null)
        const data = [
            {
                "answer_vote": 0, 
                "id": 1, 
                "name": "team_1", 
                "opposite_team": "team_2", 
                "point": {
                    "answer": 15, 
                    "present": 85, 
                    "question": 0, 
                    "total": 100
                }, 
                "point_after_steal": {
                    "answer": 0, 
                    "present": 85, 
                    "question": 0, 
                    "total": 85
                }, 
                "question_vote": 0
            }, 

            {
                "answer_vote": 0, 
                "id": 2, 
                "name": "team_2", 
                "opposite_team": "team_1", 
                "point": {
                    "answer": 0, 
                    "present": 0, 
                    "question": 16, 
                    "total": 16
                }, 
                "point_after_steal": {
                    "answer": 0, 
                    "present": 0, 
                    "question": 16, 
                    "total": 31
                }, 
                "question_vote": 2
            },
            {
                "answer_vote": 0, 
                "id": 1, 
                "name": "team_1", 
                "opposite_team": "team_2", 
                "point": {
                    "answer": 15, 
                    "present": 85, 
                    "question": 0, 
                    "total": 100
                }, 
                "point_after_steal": {
                    "answer": 0, 
                    "present": 85, 
                    "question": 0, 
                    "total": 85
                }, 
                "question_vote": 0
            }, 

            {
                "answer_vote": 0, 
                "id": 2, 
                "name": "team_2", 
                "opposite_team": "team_1", 
                "point": {
                    "answer": 0, 
                    "present": 0, 
                    "question": 16, 
                    "total": 16
                }, 
                "point_after_steal": {
                    "answer": 0, 
                    "present": 0, 
                    "question": 16, 
                    "total": 31
                }, 
                "question_vote": 2
            },
            {
                "answer_vote": 0, 
                "id": 1, 
                "name": "team_1", 
                "opposite_team": "team_2", 
                "point": {
                    "answer": 15, 
                    "present": 85, 
                    "question": 0, 
                    "total": 100
                }, 
                "point_after_steal": {
                    "answer": 0, 
                    "present": 85, 
                    "question": 0, 
                    "total": 85
                }, 
                "question_vote": 0
            }, 

            {
                "answer_vote": 0, 
                "id": 2, 
                "name": "team_2", 
                "opposite_team": "team_1", 
                "point": {
                    "answer": 0, 
                    "present": 0, 
                    "question": 16, 
                    "total": 16
                }, 
                "point_after_steal": {
                    "answer": 0, 
                    "present": 0, 
                    "question": 16, 
                    "total": 31
                }, 
                "question_vote": 2
            },
        ]

        const addClass = (index) => {
            for(let i = 0; i < data.length; i++){
                if(data[index]['name'] == data[i]['opposite_team']){
                    
                    if(data[index]['answer_vote'] > data[i]['question_vote']){
                        const answer_vote_element = document.getElementsByClassName('question-vote')[i]
                        answer_vote_element.setAttribute("id", "reduce");
                        answer_vote_element.setAttribute("data-id", i);
                    }
                    else if(data[index]['question_vote'] > data[i]['answer_vote']){
                        const question_vote_element = document.getElementsByClassName('answer-vote')[i]
                        console.log('i: ', i)
                        question_vote_element.setAttribute("id", "reduce");
                        question_vote_element.setAttribute("data-id", i);
                    }
           
                    break
                } 
            }
        }
        
        let timeOutId = null;
        const updateData = (event) => {
            const index = event.target.getAttribute("data-id")
            addClass(index)
            if (timeOutId != null) {
                clearTimeout(timeOutId);
            }
            
            const id = setTimeout(() => {
                flyMeTo('reduce', event.target, true);
                console.log('run');
            }, 400);
            timeOutId = id;
        }

        function flyMeTo(elem, destination, prepend) {
            var $elem = $('#' + elem);
            $elem.parent().append( '<p class="fw-normal mb-1 answer-vote">0</p>' )
            var $dest = $(destination);
            const id_destination = $dest.attr('data-id')
            const id_start = $elem.attr('data-id')
            const total_point_destination_element = document.getElementsByClassName('total-point')[id_destination]
            const total_point_start_element = document.getElementsByClassName('total-point')[id_start]
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
                    $dest.text($elem.text());
                    total_point_destination_element.style.color = '#32a732';
                    total_point_destination_element.style.fontWeight = '600';
                    total_point_destination_element.style.fontSize = '1rem';
                    total_point_start_element.style.color = '#ff0000';
                    total_point_start_element.style.fontWeight = '600';
                    total_point_start_element.style.fontSize = '1rem';
                    countTo(data[id_destination]['point']['total'], data[id_destination]['point_after_steal']['total'], total_point_destination_element)
                    countTo(data[id_start]['point']['total'], data[id_start]['point_after_steal']['total'], total_point_start_element)
                });
                $dest.text('???');
            }else {
                $dest.text('0')
                $dest.css({color:'red'});
                // countTo(data[id_destination]['point']['total'], data[id_destination]['point_after_steal']['total'], total_point_element)
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
  