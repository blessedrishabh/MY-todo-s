# MY-todo-s
web application
//HTML FILE


<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet"
            integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">

    </head>
    <body>
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">MY todo's</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                    data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent"
                    aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                        <li class="nav-item">
                            <a class="nav-link active" aria-current="page" href="#">Home</a>
                        </li>

                    </ul>
                    <form class="d-flex">
                        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
                        <button class="btn btn-outline-success" type="submit">Search</button>
                    </form>
                </div>
            </div>
        </nav>

        <div class="card">

            <div class="card-body">
                <h5 class="card-title">New todo</h5>
                <div class="mb-3">
                    <label for="exampleFormControlTextarea1" class="form-label">Add your todo</label>
                    <textarea class="form-control" id="addtxt" rows="3"></textarea>
                </div>
                <button id="addbtn" class="btn btn-primary">Create todo</button>
                <hr>
                <h1>Your todo's</h1>
                <hr>
                <div id="notes" class="row container-fluid">
                    <div class="row container-fluid">
                        <div class="card my-5 mx-2" style="width: 18rem;">

                            <div class="card-body">
                                <h5 class="card-title">todo</h5>

                                <button class="btn btn-primary">Delete todo</button>
                            </div>

                        </div>
                    </div>
                </div>

            </div>
        </div>



        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js"
            integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj"
            crossorigin="anonymous"></script>
        <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.3/dist/umd/popper.min.js"
            integrity="sha384-eMNCOe7tC1doHpGoWe/6oMVemdAVTMs2xqW4mwXrXsW0L84Iytr2wi5v2QjrP/xp"
            crossorigin="anonymous"></script>
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.min.js"
            integrity="sha384-cn7l7gDp0eyniUwwAZgrzD06kc/tftFf19TOAs2zVinnD/C7E91j9yyk5//jjpt/"
            crossorigin="anonymous"></script>


    </body>
    <script src="index.js"></script>
</html>




//JAVASCRIPT FILE



console.log("welcome");
shownotes();
let addBtn = document.getElementById("addbtn");
addBtn.addEventListener("click", function (e) {
    let addTxt = document.getElementById("addtxt");
    let notes = localStorage.getItem("notes");
    if (notes == null) {
        notesobj = [];
    }
    else {
        notesobj = JSON.parse(notes);
    }
    notesobj.push(addTxt.value);
    localStorage.setItem("notes", JSON.stringify(notesobj));
    addTxt.value = "";
    console.log(notesobj);
    shownotes();
})
function shownotes() {
    let notes = localStorage.getItem("notes");
    if (notes == null) {
        notesobj = [];
    }
    else {
        notesobj = JSON.parse(notes);
    }
    let html = "";
    notesobj.forEach(function (element, index) {
        html += `
        <div id="notes" class="row container-fluid">
        <div class="row container-fluid">
            <div class="card my-5 mx-2" style="width: 18rem;">

                <div class="card-body">
                <h5 class = "card-title">note${index + 1}</h5>
                <p class = "card-text">${element}</p>

                    <button id = "${index}" onclick = "deletenote(this.id)"  class="btn btn-primary">Delete todo</button>
                </div>

            </div>
        </div>
    </div>
            
            `

    });
    let noteselm = document.getElementById("notes");
    if (notesobj.length != 0) {
        noteselm.innerHTML = html;
    }

}
function deletenote(index){
    let notes = localStorage.getItem("notes");
    if (notes == null) {
        notesobj = [];
    }
    else {
        notesobj = JSON.parse(notes);
    }
    notesobj.splice(index, 1);
    localStorage.setItem("notes", JSON.stringify(notesobj));
    shownotes();

}
