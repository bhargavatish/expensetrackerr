# expensetrackerr
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ExpenseTracker</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta/css/bootstrap.min.css"
        integrity="sha384-/Y6pD6FV/Vv2HJnA6t+vslU6fwYXjCFtcEpHbNJ0lyAFsXTsjBbfaDjzALeQsN6M" crossorigin="anonymous">
</head>
<script src="https://cdnjs.cloudflare.com/ajax/libs/axios/0.19.0/axios.min.js"></script>

<body>
    <header class="">
        <div class="container col-12">
            <h1 id="main-title" class="bg-success  p-4 mb-3 text-white title">
                Expense Tracker
            </h1>
        </div>
    </header>
    <div class="container card card-body col-11 " id="main-card">
        <form action="" id="main-form" class="form-inline p-4">
            <label for="exp" class="mr-1">
                <h6>Choose-ExpenseAmount</h6>
            </label>
            <input type="number" id="exp" class=" form-control mr-2 placeholder=" 100>
            <h6 class="mr-1">Choose-Category</h6>
            <select name="category" id="caty" class="form-control mr-2">
                <option value="">Select</option>
                <option value="Movie">Movie</option>
                <option value="Travel">Travel</option>
                <option value="Outlet">Outlet</option>
            </select>
            <label for="desc">
                <h6 class="mr-1">Choose-Description</h6>
            </label>
            <input type="text" id="desc" class="form-control mr-2" placeholder="Type-Description">
            <input type="submit" id="add-expense" value="Add Expense" class="bg-dark text-white btn">
            <div class="container">
                <ul class="list-group p-3" id="main-list">
                </ul>
            </div>
        </form>
    </div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/axios/0.19.0/axios.min.js"></script>
<script>
    var form = document.querySelector('#main-form');
    var Add = document.querySelector('#add-expense')
    Add.addEventListener('click', addExpense);
    var num = 0;

    function addExpense(e) {
        e.preventDefault();

        num = num + 1;
        let amt = document.querySelector('#exp').value;
        let caty = document.querySelector('#caty').value;;
        let desc = document.querySelector('#desc').value;;
        var ul = document.querySelector('#main-list');
        var li = document.createElement('li');
        li.className = 'list-group-item';
        let liAmt = document.createTextNode(amt + ' - ');
        let liCaty = document.createTextNode(caty + ' - ');
        let liDesc = document.createTextNode(desc);

        let myExpense = {
            amount: amt,
            category: caty,
            description: desc
        };
        // Stringfy the object
        let expDetails = JSON.stringify(myExpense); let temp = num;

        //Append the Child

        li.appendChild(liAmt); li.appendChild(liCaty); li.appendChild(liDesc);
        ul.appendChild(li);
        // localStorage.setItem(temp, expDetails);
        axios.post('https://crudcrud.com/api/5104555d85c449c4ac17f417cae6fe5a/appointment',myExpense)
        .then((res) => console.log(res))
        .catch((err) => console.log(err));

        document.querySelector('#exp').value = '';
        document.querySelector('#caty').value ='';
        document.querySelector('#desc').value ='';

        //create delete
        var delBtn = document.createElement('input'); delBtn.type = 'button'
        delBtn.value = 'Delete Expense';
        delBtn.classList = 'btn btn-sm btn-warning float-right text-white delete mr-2';

        delBtn.onclick = function (e) {
            e.preventDefault();
            var del = e.target.parentElement;
            localStorage.removeItem(temp);
            ul.removeChild(del);
        }
        li.appendChild(delBtn);

        //create edit
        var edit = document.createElement('input'); edit.type = 'button';
        edit.value = 'Edit Expense ';
        edit.classList = 'btn btn-dark text-white float-right btn-sm Edit mr-2';

        edit.onclick = function (e) {
            e.preventDefault();
            var onEdit = e.target.parentElement;
            localStorage.removeItem(temp);
            ul.removeChild(onEdit);

            //restore fields
            document.querySelector('#exp').value = amt;
            document.querySelector('#caty').value = caty;
            document.querySelector('#desc').value = desc;
        }
        li.appendChild(edit);
    }
</script>
</body>
</html>
