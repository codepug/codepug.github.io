---
layout: home
title: Riak & jQuery DataTables - Overview Presentation
permalink: /wiki/riak-and-datatables
---

## Riak & jQuery DataTables - Overview Presentation

This page contains a link to presentation slides that can be used to share our excitement about jQuery DataTables used in conjunction with a noSQL database solution supplying JSON.  

### Presentation Information
  * **Title:**        Riak & jQuery DataTables: Will they blend?  
           
  * **Description:**  This presentation will provide an overview of the implications of mixing jQuery DataTables with Riak to quickly architect a feature rich application suiting a wide variety of needs.

  * **Duration:**      45 minutes + question/answer time

### Link to Slides

  * Open Office [riak-and-datatables.odp](/downloads/riak-and-datatables.odp)
  * PDF [riak-and-datatables.pdf](/downloads/riak-and-datatables.pdf)

### Code Examples

01_basic.html - Simple demonstration of jQuery DataTables
<code>
<html>
<link rel="stylesheet" type="text/css" href="http://cdn.datatables.net/1.10.5/css/jquery.dataTables.css">
<script type="text/javascript" charset="utf8" src="http://code.jquery.com/jquery-1.11.1.min.js"></script>
<script type="text/javascript" charset="utf8" src="http://cdn.datatables.net/1.10.5/js/jquery.dataTables.min.js"></script>

<script>
    $(document).ready(function () {
        $('#myTable').dataTable();
    });
</script>
<table id="myTable">
    <thead>
        <tr>
            <td>Group</td>
            <td>Subject</td>
            <td>Last Used</td>
        </tr>
    </thead>
    <tbody>
    <tr><td>Event </td><td>I: Thank You </td><td>0000-00-00 00:00:00</td></tr>
    <tr><td>Event </td><td>Q: Request for Help </td><td>0000-00-00 00:00:00</td></tr>
    <tr><td>Event </td><td>Q: Schedule Follow-up </td><td>0000-00-00 00:00:00</td></tr>
    <tr><td>Time </td><td>Q: Vacation Request </td><td>0000-00-00 00:00:00</td></tr>
    <tr><td>Time </td><td>I: Vacation Reminder </td><td>0000-00-00 00:00:00</td></tr>
    <tr><td>Time </td><td>I: Out Sick </td><td>0000-00-00 00:00:00</td></tr>
    </tbody>
</table>

</html>
</code>

02_ajax.html - Example pulling data from an AJAX request
<code>
<html>
<link rel="stylesheet" type="text/css" href="http://cdn.datatables.net/1.10.5/css/jquery.dataTables.css">
<script type="text/javascript" charset="utf8" src="http://code.jquery.com/jquery-1.11.1.min.js"></script>
<script type="text/javascript" charset="utf8" src="http://cdn.datatables.net/1.10.5/js/jquery.dataTables.min.js"></script>

<script>
    $(document).ready(function () {
        $('#myTable').dataTable({
            "ajax": {
                "url": "02_ajax.txt",
                "dataSrc": "",
            },
            "columns": [
                {
                    "data": "group"
                },
                {
                    "data": "subject"
                },
                {
                    "data": "lastUsed"
                }]
        });
    });
</script>
<table id="myTable">
    <thead>
        <tr>
            <td>Group</td>
            <td>Subject</td>
            <td>Last Used</td>
        </tr>
    </thead>
    
</table>

</html>
</code>

02_ajax.txt - Data for AJAX example
<code>
[
{"group":"Time","subject":"Q: Vacation Request","lastUsed":"0000-00-00 00:00:00"},
{"group":"Time","subject":"I: Vacation Reminder","lastUsed":"0000-00-00 00:00:00"},
{"group":"Time","subject":"I: Out Sick","lastUsed":"0000-00-00 00:00:00"},
{"group":"Event","subject":"I: Thank You","lastUsed":"0000-00-00 00:00:00"},
{"group":"Event","subject":"Q: Request for Help","lastUsed":"0000-00-00 00:00:00"},
{"group":"Event","subject":"Q: Schedule Follow-up","lastUsed":"0000-00-00 00:00:00"}
]
</code>

03_css.html - Beautifying our tables with CSS styles
<code>
<html>
<link rel="stylesheet" type="text/css" href="http://cdn.datatables.net/1.10.5/css/jquery.dataTables.css">
<script type="text/javascript" charset="utf8" src="http://code.jquery.com/jquery-1.11.1.min.js"></script>
<script type="text/javascript" charset="utf8" src="http://cdn.datatables.net/1.10.5/js/jquery.dataTables.min.js"></script>

    <style>
    table.dataTable thead {
        background-color: #07c;
        color: #fff;
        font-weight: bold;
    }
    
    table.dataTable {
        border: solid 1px #000;
        font-family: sans-serif;
        font-size: 10pt;
    }
    
    table.dataTable tbody tr td {
       padding-left: 1.5em;   
    }
    
    table.dataTable tr.even {
        background-color: #eee;
    }
    
    table.dataTable tbody tr:hover {
        background-color: #dde;
    }
    
    table.dataTable tbody tr.selected {
        background-color: #aaa;   
    }
</style>
    
<script>
    $(document).ready(function () {
        $('#myTable').dataTable({

        });
    });
</script>
<table id="myTable">
    <thead>
        <tr>
            <td>Group</td>
            <td>Subject</td>
            <td>Last Used</td>
        </tr>
    </thead>
    <tbody>
    <tr><td>Event </td><td>I: Thank You </td><td>0000-00-00 00:00:00</td></tr>
        <tr><td>Event </td><td>Q: Request for Help </td><td>0000-00-00 00:00:00</td>
        <tr><td>Event </td><td>Q: Schedule Follow-up </td><td>0000-00-00 00:00:00</td>
        <tr><td>Time </td><td>Q: Vacation Request </td><td>0000-00-00 00:00:00</td>
        <tr><td>Time </td><td>I: Vacation Reminder </td><td>0000-00-00 00:00:00</td>
        <tr><td>Time </td><td>I: Out Sick </td><td>0000-00-00 00:00:00</td></tr>
    </tbody>
</table>

</html>
</code>

04_page.html - Example showing various pagination options
<code>
<html>
<link rel="stylesheet" type="text/css" href="http://cdn.datatables.net/1.10.5/css/jquery.dataTables.css">
<script type="text/javascript" charset="utf8" src="http://code.jquery.com/jquery-1.11.1.min.js"></script>
<script type="text/javascript" charset="utf8" src="http://cdn.datatables.net/1.10.5/js/jquery.dataTables.min.js"></script>

    <style>
    table.dataTable thead {
        background-color: #07c;
        color: #fff;
        font-weight: bold;
    }
    
    table.dataTable {
        border: solid 1px #000;
        font-family: sans-serif;
        font-size: 10pt;
    }
    
    table.dataTable tbody tr td {
       padding-left: 1.5em;   
    }
    
    table.dataTable tr.even {
        background-color: #eee;
    }
    
    table.dataTable tbody tr:hover {
        background-color: #dde;
    }
    
    table.dataTable tbody tr.selected {
        background-color: #aaa;   
    }
</style>
    
<script>
    $(document).ready(function () {
        $('#myTable').dataTable({
            "pageLength": 4,
            lengthChange: false,
            fnDrawCallback: function (pref) {
                var columnCount = $(this).children('thead').children('tr').children('th').length,
                    missing = pref._iDisplayLength - $(this).children('tbody').children('tr').length,
                    i;
                for (i = 0; i < missing; i++) {
                    $(this).append('<tr class="space"><td colspan="' + columnCount + '">&nbsp;</td></tr>');
                }
            }
        });
    });
</script>
<table id="myTable">
    <thead>
        <tr>
            <td>Group</td>
            <td>Subject</td>
            <td>Last Used</td>
        </tr>
    </thead>
    <tbody>
    <tr><td>Event </td><td>I: Thank You </td><td>0000-00-00 00:00:00</td></tr>
        <tr><td>Event </td><td>Q: Request for Help </td><td>0000-00-00 00:00:00</td>
        <tr><td>Event </td><td>Q: Schedule Follow-up </td><td>0000-00-00 00:00:00</td>
        <tr><td>Time </td><td>Q: Vacation Request </td><td>0000-00-00 00:00:00</td>
        <tr><td>Time </td><td>I: Vacation Reminder </td><td>0000-00-00 00:00:00</td>
        <tr><td>Time </td><td>I: Out Sick </td><td>0000-00-00 00:00:00</td></tr>
    </tbody>
</table>

</html>
</code>

05_select.html - Enabling the ability to select a row in a table
<code>
<html>
<link rel="stylesheet" type="text/css" href="http://cdn.datatables.net/1.10.5/css/jquery.dataTables.css">
<script type="text/javascript" charset="utf8" src="http://code.jquery.com/jquery-1.11.1.min.js"></script>
<script type="text/javascript" charset="utf8" src="http://cdn.datatables.net/1.10.5/js/jquery.dataTables.min.js"></script>

<style>
    table.dataTable tbody tr.selected {
        background-color: #aaa;   
    }
</style>
    
<script>
    $(document).ready(function () {
        var table = $('#myTable').dataTable();
        $('#myTable tbody').on('click', 'tr', function () {
            $(this).toggleClass('selected');
            table.$('tr.selected').not(this).removeClass('selected');
        });
        $('#myTable').click(function () {
            table.row('.selected').remove().draw(false);
        });
    });
</script>
<table id="myTable">
    <thead>
        <tr>
            <td>Group</td>
            <td>Subject</td>
            <td>Last Used</td>
        </tr>
    </thead>
    <tbody>
    <tr><td>Event </td><td>I: Thank You </td><td>0000-00-00 00:00:00</td></tr>
        <tr><td>Event </td><td>Q: Request for Help </td><td>0000-00-00 00:00:00</td>
        <tr><td>Event </td><td>Q: Schedule Follow-up </td><td>0000-00-00 00:00:00</td>
        <tr><td>Time </td><td>Q: Vacation Request </td><td>0000-00-00 00:00:00</td>
        <tr><td>Time </td><td>I: Vacation Reminder </td><td>0000-00-00 00:00:00</td>
        <tr><td>Time </td><td>I: Out Sick </td><td>0000-00-00 00:00:00</td></tr>
    </tbody>
</table>

</html>
</code>

06_cells.html - Combining content from multiple columns into one
<code>
<html>
<link rel="stylesheet" type="text/css" href="http://cdn.datatables.net/1.10.5/css/jquery.dataTables.css">
<script type="text/javascript" charset="utf8" src="http://code.jquery.com/jquery-1.11.1.min.js"></script>
<script type="text/javascript" charset="utf8" src="http://cdn.datatables.net/1.10.5/js/jquery.dataTables.min.js"></script>

<script>
    $(document).ready(function () {
        $('#myTable').dataTable({
            "columnDefs": [
                {
                    "render": function (data, type, row) {
                        return '<a href="mailto:' + row[0] + '">' + data + '</a>';
                    },
                    "targets": 1
                },
                {
                    "visible": false,
                    "targets": [0]
                },
                {
                    "width": "25%",
                    "targets": 2
                }
        ]
        });
    });
</script>
<table id="myTable">
    <thead>
        <tr>
            <td>Group</td>
            <td>Subject</td>
            <td>Last Used</td>
        </tr>
    </thead>
    <tbody>
    <tr><td>Event </td><td>I: Thank You </td><td>0000-00-00 00:00:00</td></tr>
    <tr><td>Event </td><td>Q: Request for Help </td><td>0000-00-00 00:00:00</td></tr>
    <tr><td>Event </td><td>Q: Schedule Follow-up </td><td>0000-00-00 00:00:00</td></tr>
    <tr><td>Time </td><td>Q: Vacation Request </td><td>0000-00-00 00:00:00</td></tr>
    <tr><td>Time </td><td>I: Vacation Reminder </td><td>0000-00-00 00:00:00</td></tr>
    <tr><td>Time </td><td>I: Out Sick </td><td>0000-00-00 00:00:00</td></tr>
    </tbody>
</table>

</html>
</code>