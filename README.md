# File Upload Example
We will discuss about uploading file techniques in vb.NET.
## Step 1: Add File open dialog box to your form.
-Go to toolbox and add one OpenFileDialog box.
## Step 2: Add picture box to your form.
-Go to ToolBox and add the picture box to your form. 
## Step 3: Add Button below the PictureBox.
- Add picture box and add text "Load Image" on the button. 
- on click event of that button. add fllowing code.
````
Private Sub Button2_Click(sender As Object, e As EventArgs) Handles Button2.Click
        Try
            OpenFileDialog1.FileName = ""
            If OpenFileDialog1.ShowDialog() = DialogResult.OK Then
                PictureBox1.Image = Image.FromFile(OpenFileDialog1.FileName)
            End If
        Catch ex As Exception

        End Try
    End Sub
````
## After completing the above condition you can load image on your form. 
Now you can store the image to the database using insert operation. Remember you have to add column with image datatype in your table in order to store image.  
For example: 
````
            Dim sqlcmd As New SqlCommand()
            sqlcmd.Connection = DBConnection.GetServerConnection()
            Dim sqlstring As String
            Dim ms As New MemoryStream
            PictureBox1.Image.Save(ms, PictureBox1.Image.RawFormat)
            sqlstring = "insert into people(name,address,image) values('" & Me.TextBox2.Text & "','" & Me.TextBox3.Text & "',@img)"
            sqlcmd.CommandText = sqlstring
            sqlcmd.Parameters.AddWithValue("@img", ms.ToArray)
            sqlcmd.ExecuteNonQuery()
````
ms is memory stream where picture box image will be stored on it. @img stores the image value 
you can find the source code here. 
https://oxfordcollegeedunp-my.sharepoint.com/:u:/g/personal/itsupport_oxfordcollege_edu_np/EYv2MRcLZxxCpoIlOBLhcrIBoqF38via2fHP4igOYiLsqg?e=1EMrAL
For Print Demo:
find the source code here: https://oxfordcollegeedunp-my.sharepoint.com/:u:/g/personal/itsupport_oxfordcollege_edu_np/EUQq_-hyL6xLhfJFKHke1KgBeiDmtQtHCn6UJvAd7kieIA?e=hMSFS3

# To load image  form dataase.
 ````
        Dim sccmd As New SqlCommand()
        sccmd.Connection = DBConnection.GetServerConnection()
        sccmd.CommandText = "select * from people where id=" + tnumb.ToString()
        Dim dtblpeople As New DataTable()
        Dim adp As New SqlDataAdapter(sccmd)
        adp.Fill(dtblpeople)
        'display image inside picture box from database server
        Dim data As Byte() = DirectCast(dtblpeople.Rows(0)("image"), Byte())
        Dim ms As New MemoryStream(data)
        PictureBox1.Image = Image.FromStream(ms)
 ````
