<%@ Page Title="" Language="vb" AutoEventWireup="false" MasterPageFile="~/LcmfMaster.Master" CodeBehind="AddCategory.aspx.vb" Inherits="LCMF_Invent.AddCategory" %>

<%@ Register Assembly="AjaxControlToolkit" Namespace="AjaxControlToolkit" TagPrefix="ajaxToolkit" %>
<asp:Content ID="Content1" ContentPlaceHolderID="head" runat="server">
              <link href="css/sb-admin-2.min.css" rel="stylesheet">
    <link href="css/gridstyles.css" rel="stylesheet" type="text/css" />
     <link href="vendor/datatables/dataTables.bootstrap4.min.css" rel="stylesheet">
        <style type="text/css">
              

            .auto-style1 {
                text-decoration: underline;
            }
            .auto-style3 {
                width: 400px;
                height: 52px;
            }
            .auto-style5 {
                width: 400px;
            }



            </style>

</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="ContentPlaceHolder1" runat="server">
  
       <div class="card shadow mb-4 w-75" runat="server" >

                <div class="card-header py-2">
                     <h1 class="h5 mb-4 text-gray-800">Commodity Category</h1>
                  
                    </div>

                 <div class="card-body" id="dvmain" runat="server" >
                      <asp:UpdatePanel ID="UpdatePanel2" runat="server">
    <ContentTemplate>     
        <asp:Button ID="Button1" runat="server" Text="Create New Category" OnClick = "Add" class="btn btn-primary"  />
      
 
        
         <asp:Panel ID="pnlAddEdit" runat="server" CssClass="modalPopup" style = "display:none">
                
             <div class="modal-body bg-gradient-dark">
                 
                 <div class="container-fluid">
                 <div class="row">
   
                     <div class="col-sm-5 text-white font-weight-bold">  
             <label for="toloc_list">New Category:</Label>  </div>
                         <div class="col-md-5  font-weight-bold"> 
                                             <asp:TextBox ID="txtName" runat="server" width="220px" class="form-control" Height="30px" MaxLength="50" autocomplete="off"/>
                             <%--<asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" ErrorMessage="*" ForeColor="Red" ControlToValidate="txtName"></asp:RequiredFieldValidator>--%>
                         </div>
                         </div>
                 <div class="row">
                     <div class="col-sm-5 text-white font-weight-bold">  
             <label for="toloc_list">Federation <br />Commission:</Label> </div>
                         <div class="col-md-5   font-weight-bold">  
                          <div class="input-group-append">  <asp:TextBox ID="txtcp" runat="server" Width="80px" class="form-control" height="30px" MaxLength="5" autocomplete="off"/><b>%</b>
                                                  <%--<asp:RequiredFieldValidator ID="RequiredFieldValidator2" runat="server" ErrorMessage="*" ForeColor="Red" ControlToValidate="txtcp"></asp:RequiredFieldValidator>--%>

                          </div> </div>
                     </div>
           
                </div>
              <div class="modal-footer ">
                  <div class="col-md-8 offset-md-2">
                   <div class="input-group-append">  <asp:Button ID="btnAdd" runat="server" Font-Bold="True"  OnClick="Insert" Text="Save" class="btn btn-primary"/>
                         <asp:Button ID="btnCancel" class="btn btn-secondary" runat="server" Text="Cancel" OnClientClick = "return Hidepopup()"/></div></div>
                          <asp:Label ID="error_lbl" runat="server" Font-Names="Arial" Font-Size="Small" ForeColor="Red" Width="272px"></asp:Label>
                  </div></div>
       </asp:Panel>

        <asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="false" OnRowDataBound="OnRowDataBound"
            DataKeyNames="c_code" OnRowEditing="OnRowEditing" OnRowCancelingEdit="OnRowCancelingEdit" PageSize = "20" AllowPaging ="true" OnPageIndexChanging = "OnPaging"
             CssClass="table-bordered" OnRowUpdating="OnRowUpdating" OnRowDeleting="OnRowDeleting" EmptyDataText="No records has been added."
            Width="800px">
                  <AlternatingRowStyle BackColor="#f0f0f0" />
                                        <EditRowStyle BackColor="#999999" />
                                        <FooterStyle BackColor="#5D7B9D" ForeColor="White" />
                                        <HeaderStyle CssClass="bg-gradient-primary" ForeColor="White" Font-Size="12px" />
                                        <PagerStyle BackColor="#284775" ForeColor="White" HorizontalAlign="Center" />
                                        <RowStyle BackColor="#F7F6F3" ForeColor="#000000" />

                                        <Columns>
                <asp:TemplateField HeaderText="Name" ItemStyle-Width="150">
                    <ItemTemplate>
                        <asp:Label ID="lblName" runat="server" Text='<%# Eval("c_name") %>'></asp:Label>
                    </ItemTemplate>
                    <EditItemTemplate>
                        <asp:TextBox ID="txtName" runat="server" Text='<%# Eval("c_name") %>' Width="140" class="form-control form-control-user"></asp:TextBox>
                    </EditItemTemplate>
                </asp:TemplateField>

                 <asp:TemplateField HeaderText="Fed.Commission" ItemStyle-Width="150">
                    <ItemTemplate>
                        <asp:Label ID="lblcommision" runat="server" Text='<%# Eval("commision_percent") %>'></asp:Label>
                    </ItemTemplate>
                    <EditItemTemplate>
                        <asp:TextBox ID="txtcommision" runat="server" Text='<%# Eval("commision_percent") %>' Width="140" class="form-control form-control-user"></asp:TextBox>
                    </EditItemTemplate>
                </asp:TemplateField>
                
               
                 
                <asp:CommandField ButtonType="Link" ShowEditButton="true" ShowDeleteButton="false"
                    ItemStyle-Width="150" EditText="Modify" DeleteText="Remove" ControlStyle-Font-Bold="false" ControlStyle-ForeColor="#0000cc" />
            </Columns>
        </asp:GridView>
        
        <asp:LinkButton ID="lnkFake" runat="server"></asp:LinkButton>
        <ajaxToolkit:ModalPopupExtender ID="popup" runat="server"  DropShadow="false"
PopupControlID="pnlAddEdit" TargetControlID = "lnkFake"
BackgroundCssClass="modalBackground"></ajaxToolkit:ModalPopupExtender>

    </ContentTemplate>
                          <Triggers>
<asp:AsyncPostBackTrigger ControlID = "GridView1" />
<asp:AsyncPostBackTrigger ControlID = "btnAdd" />
</Triggers>
</asp:UpdatePanel>

                                                     <asp:Button ID="addbtn" runat="server"  CssClass="ui-button ui-widget ui-state-default ui-corner-all ui-button-text-only"  tabIndex="5" Text="Add" visible="false" />

                                                    <asp:Button ID="cancelbtn" runat="server"  CssClass="ui-button ui-widget ui-state-default ui-corner-all ui-button-text-only"  tabIndex="6" Text="Cancel" visible="false"/>

                    
                     
                      <asp:ValidationSummary ID="ValidationSummary1" runat="server" 
            ShowMessageBox="True" ShowSummary="False" />
        <input id="hdn_CSRF" runat="server" name="hdn_CSRF" size="10" 
            style="Z-INDEX: 105; POSITION: absolute; WIDTH: 96px; HEIGHT: 16px; TOP: 312px; LEFT: 280px" 
            type="hidden" />

                 </div>
           </div>
    
    
</asp:Content>
