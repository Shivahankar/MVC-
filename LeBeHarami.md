# MVC-
Add/Update/view in grid
View Code :=>

  @model YourAPI.ViewModels.YourModelName


<div id="tabs-e">
                            <div class="form-group">
                                <input type="button" id="BtnAddNonGovtOther" data-datac="TeraFormID" class="btn btn-info btnShow" value="ADD"><br />
                            </div>
                            @using (Ajax.BeginForm("TeraSaveActionMethode", "TeraControllerName", FormMethod.Post, new AjaxOptions { OnSuccess = "OnSuccess", InsertionMode = InsertionMode.Replace, }, new { enctype = "multipart/form-data", @id = "TeraFormID" }))
                            {
                                <input type="hidden" name="HeaderTypeID" value="2930">
                                <input type="hidden" name="DeductionTypeID" value="5">
                                @Html.HiddenFor(m => m.ID)
                                <div class="box-body">
                                    <div class="form-group">
                                        <label class="control-label" for="inputEmail3">Component Name<sup>*</sup></label>
                                        @Html.DropDownListFor(model => model.NonGovtOtherComponentID, new SelectList(Model.NonGovtdrpDwnComponentOther, "value", "text", Model.NonGovtOtherComponentID), "--Select--", new { @class = "form-control", @Required = true })
                                        @Html.HiddenFor(m => m.NonGovtOtherComponentID)
                                    </div>
                                    <div class="form-group">
                                        <label class="control-label" for="inputEmail3">Other Deduction Type<sup>*</sup></label>
                                        @Html.DropDownListFor(model => model.NonGovtOtherDeductionTypeID, new SelectList(Model.DrpNonGovtOtherDeductionType, "value", "text", Model.NonGovtOtherDeductionTypeID), "--Select--", new { @class = "form-control", @Required = true })
                                        @Html.HiddenFor(m => m.NonGovtOtherDeductionTypeID)
                                    </div>
                                    <div class="form-group">
                                        <label class="control-label" for="inputEmail3">Other Deduction Value<sup>*</sup></label>
                                        @Html.TextBoxFor(m => m.NonGovtValue, new { @class = "form-control", @Required = true, placeholder = "Other Deduction Value" })
                                    </div>
                                    <div class="form-group">
                                        <label class="control-label" for="inputEmail3">Effective From<sup>*</sup></label>
                                        @Html.TextBoxFor(m => m.NonGovtEffectiveFrom, clsConstants.DateFormat, new { @class = "form-control datepicker ", @tabindex = "-1", @readonly = "readonly", @style = "background-color:white;", placeholder = "Effective From" })
                                    </div>
                                    <div class="form-group">
                                        <label class="control-label" for="inputEmail3"> Effective To</label>
                                        @Html.TextBoxFor(m => m.NonGovtEffectiveTo, clsConstants.DateFormat, new { @class = "form-control datepicker ", @tabindex = "-1", @readonly = "readonly", @style = "background-color:white;", placeholder = "Effective To" })
                                    </div>
                                    <input type="button" id="btnSaveNonGovtDeductionDetails" value="Save" class="btn btn-primary btnSave" />
                                    <input type="button" class="btn btn-info btnHide " data-datac="BtnAddNonGovtOther" value="Cancel">
                                </div>
                            }
                            <div class="table-both-scroll">
                                <table class="table table-hover custom-table deep-blue2-head deep-lblue2-head">
                                    <thead>
                                        <tr>
                                            <th> SNO </th>
                                            <th>Deduction Type </th>
                                            <th>Other Deduction Type</th>
                                            <th>Value (<i class="fa fa-inr m-r-5 m-l-5" aria-hidden="true"></i>)</th>
                                            <th> Effective From </th>
                                            <th>Effective To</th>
                                            <th>Actions</th>
                                        </tr>
                                    </thead>
                                    <tbody id="TBodyNonOther">
                                        @if (Model.NonGovtOtherDeductionList.Count > 0)
                                        {
                                            { sno = 0; }

                                            foreach (var item in Model.NonGovtOtherDeductionList)
                                            {
                                                { sno = sno + 1; }
                                                <tr>
                                                    <td>@sno</td>
                                                    <td>
                                                        <div class="Mytooltip">
                                                            <label class="Over">@item.ComponentName</label>
                                                            <span class="tooltiptext" style="width:390px;">
                                                                <table>
                                                                    <tr><td><label>Created By</label></td> <td style="width:10px; text-align:center"><lable>:</lable></td> <td><span>@item.ToolTip.ComponentCreatedBy</span></td> </tr>
                                                                    <tr><td><label>Assigned By</label></td><td><lable>:</lable></td><td><span>@item.ToolTip.AssignedLevel </span></td>  </tr>
                                                                    <tr>
                                                                        <td><label>Calculation</label></td>
                                                                        <td><lable>:</lable></td>
                                                                        <td>
                                                                            @if (item.ToolTip.ValueType == 1)
                                                                            { <span>@item.ToolTip.ComponentValue % on basic pay</span> }
                                                                            else if (item.ToolTip.ValueType == 2)
                                                                            {<span>@item.ToolTip.ComponentValue Rupees</span>}
                                                                            else if (item.ToolTip.ValueType == 3)
                                                                            {
                                                                                if (item.ToolTip.SlabList.Count > 0)
                                                                                { <table style="float:right;">
                                                                                    @foreach (var Ite in item.ToolTip.SlabList)
                                                                                    {
                                                                                        <tr><td> @Ite.Value if Basic pay is between <span style="">@Ite.FromRange - @Ite.ToRange</span> </td></tr>}
                                                                                </table>                                                                                }
                                                                                else
                                                                                { <span>Not Defined</span>}
                                                                            }
                                                                            else
                                                                            {<span>@item.Value</span> }
                                                                        </td>
                                                                    </tr>
                                                                    <tr><td><label>Value Updated By</label></td><td><lable>:</lable></td><td><span>@item.ToolTip.ComponentUpdatedBy</span></td> </tr>
                                                                </table>
                                                            </span>
                                                        </div>
                                                    </td>
                                                    <td>@item.OtherDeductionType</td>
                                                    <td>@item.Value</td>
                                                    <td>@item.EffectiveFrom.ToString(clsConstants.ViewDateFormat)</td>
                                                    @if (item.EffectiveTo.HasValue)
                                                    {
                                                        <td>@item.EffectiveTo.Value.ToString(clsConstants.ViewDateFormat)</td>
                                                    }
                                                    else
                                                    {
                                                        <td></td>
                                                    }
                                                    <td>
                                                        </td>
                                                </tr>
                                            }
                                        }
                                        else
                                        {
                                            <tr class="info"><td colspan="7" class=" text-center">No Records Found</td></tr>
                                        }
                                    </tbody>
                                </table>
                            </div>
                        </div>


<script>
    $(".btnSave").click(function(){var from=$(this).closest("form");if(from.valid()){from.submit();}});


function FncLoadGrid(HeaderTypeID,DeductionTypeID)
    {
        //  debugger;
        $.ajax({
            url: '@Url.Action("GetTableDAta", "TeraControllerName")',
            type: 'GET',
            datatype: "json",
            async: false,
            data:
                {
                    EmployeeID:EmployeeID,
                    HeaderTypeID:HeaderTypeID,
                    DeductionTypeID:DeductionTypeID
                },
            success: function (response)
            {
                debugger;
                if(HeaderTypeID==2929&&DeductionTypeID==1)
                {    $("#TbdyGovtSub").empty();
                    $.each(response,function(num,item)
                    {

                        num = num + 1;

                        if(item.EffectiveFrom!=null)
                        {
                            var dateString = item.EffectiveFrom.substr(6);
                            var currentTime = new Date(parseInt(dateString ));
                            var month = currentTime.getMonth() + 1;
                            var day = currentTime.getDate();
                            var year = currentTime.getFullYear();
                            if(day<10)
                                day="0"+day;
                            var date = day + "-" + monthNames[month] + "-" + year;
                            item.EffectiveFrom=date;
                        }

                        if(item.EffectiveTo!=null)
                        {
                            var dateString = item.EffectiveTo.substr(6);
                            var currentTime = new Date(parseInt(dateString ));
                            var month = currentTime.getMonth() + 1;
                            var day = currentTime.getDate();
                            var year = currentTime.getFullYear();
                            if(day<10)
                                day="0"+day;
                            var date = day + "-" + monthNames[month] + "-" + year;
                            item.EffectiveTo=date;
                        }else{
                            item.EffectiveTo='';
                        }
                        $('#TbdyGovtSub').append('<tr><td>' + num + '</td><td>' + item.ComponentName + '</td><td>' + item.Value + '</td><td>' + item.EffectiveFrom + '</td> <td>' + item.EffectiveTo + '</td><td><a class="fa fa-history btn btn-xs btn-default" data-ajax="true" data-ajax-mode="replace" data-ajax-success="Success" data-ajax-update="#historyDialog" data-toggle="tooltip" href="/TeraControllerName/GetComponentHistory?CID='+item.ComponentID +'&amp;EmpId='+@ViewBag.EmployeeID +'" title="View History"> </a></td></tr>'); @*//<td>'+@Ajax.ActionLink(" ", "GetComponentHistory", "TeraControllerName", new { CID = item.ComponentID, EmpId = ViewBag.EmployeeID }, new AjaxOptions { OnSuccess = "Success", UpdateTargetId = "historyDialog" }, new { @class = "fa fa-history btn btn-xs btn-default", @data_toggle = "tooltip", @title = "View History" })+'</td>*@
                    })
                }
}};





function OnSuccess(res) {if (res.Status == true) {$("#CommonDialogStatus").html(''); $("#CommonDialogStatus").html(res.ResponseMessage); $("#CommonDialog").dialog("open");}
        $("#TeraFormID").find("[name='HeaderTypeID']").val();$("#TeraFormID").find("[name='DeductionTypeID']").val();
        FncLoadGrid($("#TeraFormID").find("[name='HeaderTypeID']").val(),$("#TeraFormID").find("[name='DeductionTypeID']").val()); }


<script/>



Web Controller:

[HttpPost]
        public ActionResult TeraSaveActionMethode(YourModelName obj)
        {
            try
            {

                var model = clsAPICalls.PostDataWithResponse<YourModelNames>(obj, "api/Controller/TeraSaveActionMethode");
                return Json(model, JsonRequestBehavior.AllowGet);

            }
            catch (Exception ex)
            {
                return View("Error");
            }
        }


API:

 [HttpGet]
        [Route("api/Controller/TeraSaveActionMethode")]
        public IHttpActionResult TeraSaveActionMethode(YourModelName obj)
        {
            try
            {
                 var result = TeraRepository.Methodetogetdata(obj);
                return Ok(result);
            }
            catch (Exception ex)
            {
                return null;
            }
        }
