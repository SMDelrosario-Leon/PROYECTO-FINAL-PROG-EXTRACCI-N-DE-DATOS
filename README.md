# PROYECTO-FINAL-PROG-EXTRACCI-N-DE-DATOS
EXTRACCIÓN DE DATOS DE TWITTER Y ALMACENARLOS A LA BASE DE DATOS 
CÓDIGO DE EXTRACCIÓN DE DATOS TWITTER
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
 
 
package ctruser;
import java.util.List;
import twitter4j.Status;
import twitter4j.TwitterException;
import twitter4j.TwitterFactory;
import twitter4j.User;
import twitter4j.conf.ConfigurationBuilder;

/**
 *
 * @author hp
 */
 
 
 
public class TWITTER_inf {
public static void main(String[] args) throws TwitterException {
        try {
      ConfigurationBuilder configurationBuilder= new ConfigurationBuilder();
      configurationBuilder.setDebugEnabled(true)
              .setOAuthConsumerKey("6Y2wTJrrlDRnlyUkj9ngrOhqO")
              .setOAuthConsumerSecret("OOfHpGoeLz73jNqnesW4Ngmjy9BK4aIIlVnoFhiwgO3Xvr3wXy")
              .setOAuthAccessToken("2729481099-CHe5T7QwQcTlYxhKgUj9gotk7H3s1LeONXTk1tL")
              .setOAuthAccessTokenSecret("0N8HgMy3gFpw9ojwbakueCgvNSGiaRz7P0bEL0z7vlNBc");
      TwitterFactory tf=new TwitterFactory(configurationBuilder.build());
      twitter4j.Twitter twitter=tf.getInstance();
     
           User usuari = twitter.verifyCredentials();
		 
		 System.out.println("Nombre: " + usuari.getName());
		 System.out.println("Descripcion: " + usuari.getDescription());
		 System.out.println("Id Usuario: " + usuari.getId());
		 System.out.println("Numero de Seguidores: " + usuari.getFollowersCount());
                 System.out.println("Numero de amigos: " + usuari.getFriendsCount());
               
                  System.out.println("\n");
                 
                  List<Status> status=twitter.getHomeTimeline();
      for(Status s:status){
          
                 System.out.println(s.getUser().getURL()+" ------"+"@"+s.getUser().getName()+" ----------"+s.getText());
                    
                 
      }
      
   
    }catch (TwitterException te) {
	            te.printStackTrace();
	            System.out.println("Error en la conexion: " + te.getMessage()); 
    }
        
    }
}
CÓDIGO DE CONSULTAS EN LA TABLA DE LA BASE DE DATOS
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package ctruser;


import com.mysql.jdbc.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

/**
 *
 * @author ShirleyDelRosario
 */
public class usuario {//libros
    
   private final Connection ssmp;
    
   
   public usuario(){
       ssmp = (Connection) SSMP.getConnection();
   }

   public int insertaUse(){
       
       int r=0;
       String consulta= "insert into persona values(SELECT * FROM `persona` WHERE 1)";// 
       try{
           Statement stm =(Statement) ssmp.createStatement(); 
           //ejecutar el insert
           r= stm.executeUpdate(consulta);
           
       }catch(SQLException e){
           System.out.println(e);
       }finally{
             return r; 
       }    
    
   }
   
    public ResultSet getConsulta() {
        
        ResultSet rs=null;
         try{
             
        Statement stm =(Statement) ssmp.createStatement(); 
        
        rs =stm.executeQuery("SELECT * FROM `persona` WHERE 1");// realiza la consulta que esta en Wampersaerver
        
    }catch(SQLException e){
        System.out.print(e);
    }
        return rs;
    }
    
    //ELIMINAR USUARIO
      public int eliminaUse(String id){
       
       int r=0;
       String consulta= "DELETE FROM `persona` WHERE `persona`.`id`=" + id;//DELETE FROM `persona` WHERE `persona`.`id` = 13;SE CONCATENA
       try{
           Statement stm =(Statement) ssmp.createStatement(); 
           //ejecutar el insert
           r= stm.executeUpdate(consulta);
           
       }catch(SQLException e){
           System.out.println(e);
       }finally{
             return r; 
       }    
    
   }
    
      
   
      
}
CÓDIGO DE CONEXIÓN A LA BASE DE DATOS

package ctruser;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class SSMP {
 
 private static final String URL= "jdbc:mysql://localhost/gruposspm";
 
//private static final String URL= "jdbc:mysql://localhost/info_twitter";      
 
 private static final String USERNAME="root";
 private static final String PASSWORD="";
 
 PreparedStatement ps;
 
 public static Connection getConnection(){
     Connection conectar=null;
        try{
         Class.forName("com.mysql.jdbc.Driver");
     //conectar= (Connection)DriverManager.getConnection("jdbc:mysql://localhost/login","root","");   
     conectar= (Connection)DriverManager.getConnection( URL,USERNAME, PASSWORD);
         
     }catch(ClassNotFoundException | SQLException e){
     System.out.println("Error al crear la conexion");
 }
    return conectar;      
}

    Connection ctruser() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }
}

CÓDIGO AGUSUARIO
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package ctruser;

//import static ctruser.SSMP.getConnection;
import java.awt.HeadlessException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import javax.swing.JOptionPane;

/**
 *
 * @author ShirleyDelRosario
 */
public class AGusuario extends javax.swing.JFrame {
    private final IngresoForm use = null;
    
SSMP cc= new SSMP();
Connection con =SSMP.getConnection();
PreparedStatement ps;
ResultSet rs;

    /**
     * Creates new form AGusuario
     */
    public AGusuario() {
        initComponents();
        
       this.setTitle("Registro usuario");
       this.setLocation(200,100);//centramos el jframe con titulo
        
    }

    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        txtUsuario = new javax.swing.JTextField();
        jLabel1 = new javax.swing.JLabel();
        jLabel2 = new javax.swing.JLabel();
        txtPass = new javax.swing.JPasswordField();
        btnAgregar = new javax.swing.JButton();
        txtnombre = new javax.swing.JTextField();
        txtId_usuario = new javax.swing.JTextField();
        txtseguidores = new javax.swing.JTextField();
        txtamigos = new javax.swing.JTextField();
        jLabel3 = new javax.swing.JLabel();
        jLabel4 = new javax.swing.JLabel();
        lblIdUsuario = new javax.swing.JLabel();
        txtID = new javax.swing.JTextField();
        txtid = new javax.swing.JLabel();
        btnconectar = new javax.swing.JButton();
        jLabel6 = new javax.swing.JLabel();
        lblestado = new javax.swing.JLabel();
        jLabel8 = new javax.swing.JLabel();
        btnlimpiar = new javax.swing.JButton();
        btnregresar = new javax.swing.JButton();
        jLabel5 = new javax.swing.JLabel();
        jSeparator1 = new javax.swing.JSeparator();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
        setBackground(new java.awt.Color(255, 255, 204));
        addMouseListener(new java.awt.event.MouseAdapter() {
            public void mouseClicked(java.awt.event.MouseEvent evt) {
                formMouseClicked(evt);
            }
        });

        jLabel1.setFont(new java.awt.Font("Arial Black", 0, 11)); // NOI18N
        jLabel1.setText("NOMBRE");

        jLabel2.setFont(new java.awt.Font("Arial Black", 0, 11)); // NOI18N
        jLabel2.setText("CLAVE");

        txtPass.setText("jPasswordField1");

        btnAgregar.setFont(new java.awt.Font("Arial Black", 0, 14)); // NOI18N
        btnAgregar.setForeground(new java.awt.Color(255, 102, 102));
        btnAgregar.setText("AGREGAR INFORMACION");
        btnAgregar.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnAgregarActionPerformed(evt);
            }
        });

        txtId_usuario.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                txtId_usuarioActionPerformed(evt);
            }
        });

        txtamigos.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                txtamigosActionPerformed(evt);
            }
        });

        jLabel3.setFont(new java.awt.Font("Arial Black", 0, 11)); // NOI18N
        jLabel3.setText("@ CUENTA");

        jLabel4.setFont(new java.awt.Font("Arial Black", 0, 11)); // NOI18N
        jLabel4.setText("ID TWEET");

        lblIdUsuario.setFont(new java.awt.Font("Arial Black", 0, 11)); // NOI18N
        lblIdUsuario.setText("# DE SEGUIDORES");

        txtID.setEditable(false);
        txtID.setBackground(new java.awt.Color(153, 153, 153));
        txtID.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                txtIDActionPerformed(evt);
            }
        });

        txtid.setFont(new java.awt.Font("Arial Black", 0, 12)); // NOI18N
        txtid.setText("ID");

        btnconectar.setText("CONECTAR");
        btnconectar.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnconectarActionPerformed(evt);
            }
        });

        jLabel6.setFont(new java.awt.Font("Arial Black", 0, 11)); // NOI18N
        jLabel6.setText("# DE AMIGOS");

        lblestado.setText("estado");

        jLabel8.setBackground(new java.awt.Color(255, 51, 51));
        jLabel8.setFont(new java.awt.Font("Arial Black", 0, 24)); // NOI18N
        jLabel8.setForeground(new java.awt.Color(255, 51, 51));
        jLabel8.setText("RECOPILACIÓN DE DATOS");

        btnlimpiar.setText("LIMPIAR");
        btnlimpiar.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnlimpiarActionPerformed(evt);
            }
        });

        btnregresar.setText("Regresar al inicio");
        btnregresar.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnregresarActionPerformed(evt);
            }
        });

        jLabel5.setFont(new java.awt.Font("Arial Black", 0, 24)); // NOI18N
        jLabel5.setForeground(new java.awt.Color(255, 51, 51));
        jLabel5.setText("CREAR CUENTA");

        jSeparator1.setForeground(new java.awt.Color(51, 51, 255));

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(120, 120, 120)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addGroup(layout.createSequentialGroup()
                                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                                    .addComponent(jLabel5)
                                    .addGroup(layout.createSequentialGroup()
                                        .addComponent(txtid)
                                        .addGap(251, 251, 251)
                                        .addComponent(txtID, javax.swing.GroupLayout.PREFERRED_SIZE, 41, javax.swing.GroupLayout.PREFERRED_SIZE)
                                        .addGap(13, 13, 13)))
                                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                                .addComponent(btnlimpiar))
                            .addGroup(layout.createSequentialGroup()
                                .addComponent(jLabel1)
                                .addGap(211, 211, 211)
                                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                                    .addComponent(txtPass, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                                    .addComponent(txtUsuario, javax.swing.GroupLayout.PREFERRED_SIZE, 111, javax.swing.GroupLayout.PREFERRED_SIZE)
                                    .addComponent(txtnombre, javax.swing.GroupLayout.PREFERRED_SIZE, 151, javax.swing.GroupLayout.PREFERRED_SIZE)
                                    .addComponent(txtId_usuario, javax.swing.GroupLayout.PREFERRED_SIZE, 143, javax.swing.GroupLayout.PREFERRED_SIZE))))
                        .addContainerGap())
                    .addGroup(layout.createSequentialGroup()
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(jLabel2)
                            .addGroup(layout.createSequentialGroup()
                                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                                    .addComponent(lblIdUsuario)
                                    .addComponent(jLabel6, javax.swing.GroupLayout.PREFERRED_SIZE, 113, javax.swing.GroupLayout.PREFERRED_SIZE))
                                .addGap(164, 164, 164)
                                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                                    .addComponent(txtamigos, javax.swing.GroupLayout.PREFERRED_SIZE, 111, javax.swing.GroupLayout.PREFERRED_SIZE)
                                    .addComponent(txtseguidores, javax.swing.GroupLayout.PREFERRED_SIZE, 186, javax.swing.GroupLayout.PREFERRED_SIZE)))
                            .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                                .addComponent(jLabel4)
                                .addComponent(jLabel3)))
                        .addGap(0, 0, Short.MAX_VALUE))))
            .addGroup(layout.createSequentialGroup()
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addContainerGap()
                        .addComponent(btnconectar)
                        .addGap(122, 122, 122)
                        .addComponent(btnAgregar)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                        .addComponent(btnregresar))
                    .addGroup(layout.createSequentialGroup()
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addGroup(layout.createSequentialGroup()
                                .addGap(153, 153, 153)
                                .addComponent(jLabel8))
                            .addGroup(layout.createSequentialGroup()
                                .addGap(49, 49, 49)
                                .addComponent(jSeparator1, javax.swing.GroupLayout.PREFERRED_SIZE, 582, javax.swing.GroupLayout.PREFERRED_SIZE)))
                        .addGap(0, 68, Short.MAX_VALUE)))
                .addContainerGap())
            .addGroup(layout.createSequentialGroup()
                .addGap(30, 30, 30)
                .addComponent(lblestado)
                .addGap(0, 0, Short.MAX_VALUE))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addGroup(layout.createSequentialGroup()
                                .addComponent(jLabel5)
                                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                                    .addGroup(layout.createSequentialGroup()
                                        .addGap(12, 12, 12)
                                        .addComponent(txtid))
                                    .addGroup(layout.createSequentialGroup()
                                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                                        .addComponent(txtID, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))))
                            .addGroup(layout.createSequentialGroup()
                                .addGap(26, 26, 26)
                                .addComponent(btnlimpiar)))
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(jLabel1)
                            .addComponent(txtUsuario, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                        .addGap(18, 18, 18)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(jLabel2)
                            .addComponent(txtPass, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addGroup(layout.createSequentialGroup()
                                .addGap(18, 18, 18)
                                .addComponent(jLabel3))
                            .addGroup(layout.createSequentialGroup()
                                .addGap(6, 6, 6)
                                .addComponent(txtnombre, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)))
                        .addGap(18, 18, 18)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(txtId_usuario, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(jLabel4))
                        .addGap(18, 18, 18)
                        .addComponent(jSeparator1, javax.swing.GroupLayout.PREFERRED_SIZE, 10, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                        .addComponent(jLabel8)
                        .addGap(18, 18, 18)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                            .addComponent(lblIdUsuario)
                            .addComponent(txtseguidores, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                        .addGap(18, 18, 18)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                            .addComponent(txtamigos, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(jLabel6, javax.swing.GroupLayout.PREFERRED_SIZE, 17, javax.swing.GroupLayout.PREFERRED_SIZE))
                        .addGap(18, 18, 18)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(btnregresar)
                            .addComponent(btnconectar))
                        .addGap(18, 18, 18))
                    .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                        .addComponent(btnAgregar)
                        .addGap(3, 3, 3)))
                .addComponent(lblestado)
                .addContainerGap(javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
        );

        pack();
    }// </editor-fold>                        

    private void btnAgregarActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // TODO add your handling code here:
       Agregarusuario(); 
     
    }                                          

    private void btnconectarActionPerformed(java.awt.event.ActionEvent evt) {                                            
     try{
            Class.forName("com.mysql.jdbc.Driver");
            // Nos conectamos a la bd
           Connection con= DriverManager.getConnection("jdbc:mysql://localhost/gruposspm","root","");
            // Si la conexion fue exitosa mostramos un mensaje de conexion exitosa
            if (con!=null){
                lblestado.setText("Conexion establecida");
            }
        }
        // Si la conexion NO fue exitosa mostramos un mensaje de error
        catch (ClassNotFoundException | SQLException e){
            lblestado.setText("Error de conexion" + e);
        }



        // TODO add your handling code here:
    }                                           

    private void txtIDActionPerformed(java.awt.event.ActionEvent evt) {                                      
        // TODO add your handling code here:
    }                                     

    private void txtId_usuarioActionPerformed(java.awt.event.ActionEvent evt) {                                              
        // TODO add your handling code here:
    }                                             

    private void btnlimpiarActionPerformed(java.awt.event.ActionEvent evt) {                                           
      limpiar();
    }                                          

    private void formMouseClicked(java.awt.event.MouseEvent evt) {                                  
      
     // TODO add your handling code here:
    }                                 

    private void btnregresarActionPerformed(java.awt.event.ActionEvent evt) {                                            
      MDIprincipal abrir= new MDIprincipal();
        abrir.setVisible(true);
         dispose();
        // TODO add your handling code here:
    }                                           

    private void txtamigosActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // TODO add your handling code here:
    }                                         
public void Agregarusuario(){
    
   // String clave=String.valueOf(txtPass.getPassword());
   String id=String.valueOf(txtID.getColumns()); 
    String SQL= "insert into persona (id,usuario,clave,Nombre,IdUsuario , NumSeguidores, NumAmigos) values (?,?,?,?,?,?,?)";// cambio
    try{
        PreparedStatement pst= con.prepareStatement(SQL);
      
        pst.setString(1,id);
        pst.setString(2, txtUsuario.getText());
        pst.setString(3,txtPass.getText()); 
        pst.setString(4, txtnombre.getText());// 
        pst.setString(5, txtId_usuario.getText());
        pst.setString(6, txtseguidores.getText());
        pst.setString(7, txtamigos.getText());        
        pst.executeUpdate();   
        
        JOptionPane.showMessageDialog(null,"Registro Exitoso");
    }catch(HeadlessException | SQLException e){
        JOptionPane.showMessageDialog(null,"Error de registro" + e.getMessage());
    }
   
}
//////
/*public void AgregaInf(){
    
    String id=String.valueOf(txtID1.getColumns()); 
    String SQL= "insert into persona (id,Nombre,IdUsuario , NumSeguidores, NumAmigos ) values (?,?,?,?.?)";
         try{
        PreparedStatement psta= con.prepareStatement(SQL);
        
        psta.setString(1,id);
        psta.setString(2, txtnombre.getText());// 
        psta.setString(3, txtId_usuario.getText());
        psta.setString(4, txtseguidores.getText());
        psta.setString(5, txtamigos.getText());
        psta.executeUpdate();  
        
 JOptionPane.showMessageDialog(null,"Registro Exitoso");
    }catch(HeadlessException | SQLException e){
        JOptionPane.showMessageDialog(null,"Error de registro" + e.getMessage());
    }
}
*/





   
   public void limpiar(){ // se llama en el boton limpiar
      txtid.setText("");
        txtnombre.setText("");
          txtId_usuario.setText("");
           txtseguidores.setText("");
            txtUsuario.setText("");
             txtPass.setText("               ");
              txtamigos.setText("");
    }
    
    /**
     * @param args the command line arguments
     */
    public static void main(String args[]) {
        /* Set the Nimbus look and feel */
        //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
        /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
         * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
         */
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(AGusuario.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(AGusuario.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(AGusuario.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(AGusuario.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>

        /* Create and display the form */
        java.awt.EventQueue.invokeLater(() -> {
            new AGusuario().setVisible(true);
           
            
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton btnAgregar;
    private javax.swing.JButton btnconectar;
    private javax.swing.JButton btnlimpiar;
    private javax.swing.JButton btnregresar;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel2;
    private javax.swing.JLabel jLabel3;
    private javax.swing.JLabel jLabel4;
    private javax.swing.JLabel jLabel5;
    private javax.swing.JLabel jLabel6;
    private javax.swing.JLabel jLabel8;
    private javax.swing.JSeparator jSeparator1;
    private javax.swing.JLabel lblIdUsuario;
    private javax.swing.JLabel lblestado;
    private javax.swing.JTextField txtID;
    private javax.swing.JTextField txtId_usuario;
    private javax.swing.JPasswordField txtPass;
    private javax.swing.JTextField txtUsuario;
    private javax.swing.JTextField txtamigos;
    private javax.swing.JLabel txtid;
    private javax.swing.JTextField txtnombre;
    private javax.swing.JTextField txtseguidores;
    // End of variables declaration        
}
CÓDIGO ABRIR ARCHIVO TXT
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package ctruser;

import java.io.IOException;
import java.util.logging.Level;
import java.util.logging.Logger;

/**
 *
 * @author hp
 */
public class Abre_Cualquier_Archivo extends javax.swing.JFrame {

    /**
     * Creates new form Abre_Cualquier_Archivo
     */
    public Abre_Cualquier_Archivo() {
        initComponents();
    }

    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jButton1 = new javax.swing.JButton();
        jLabel1 = new javax.swing.JLabel();
        btnExtraccion = new javax.swing.JButton();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        jButton1.setText("ABRIR INFORMACION");
        jButton1.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jButton1ActionPerformed(evt);
            }
        });

        jLabel1.setIcon(new javax.swing.ImageIcon(getClass().getResource("/TW.PNG"))); // NOI18N
        jLabel1.setText("jLabel1");

        btnExtraccion.setText("Ir a Ingreso de datos");
        btnExtraccion.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnExtraccionActionPerformed(evt);
            }
        });

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addGap(78, 78, 78)
                        .addComponent(jLabel1, javax.swing.GroupLayout.PREFERRED_SIZE, 243, javax.swing.GroupLayout.PREFERRED_SIZE))
                    .addGroup(layout.createSequentialGroup()
                        .addGap(118, 118, 118)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                            .addComponent(jButton1)
                            .addComponent(btnExtraccion))))
                .addGap(44, 100, Short.MAX_VALUE))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(30, 30, 30)
                .addComponent(jLabel1, javax.swing.GroupLayout.PREFERRED_SIZE, 215, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(48, 48, 48)
                .addComponent(jButton1)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, 39, Short.MAX_VALUE)
                .addComponent(btnExtraccion)
                .addGap(29, 29, 29))
        );

        pack();
    }// </editor-fold>                        

    private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         

        try{
        String url="C:\\Users\\hp\\OneDrive - Universidad de Guayaquil\\Escritorio\\DATOS.txt";
  
  ProcessBuilder p = new ProcessBuilder();
  p.command("cmd.exe", "/c", url);
  p.start();
    }catch (IOException ex){
       Logger.getLogger(Abre_Cualquier_Archivo.class.getName()).log(Level.SEVERE,null, ex);
     
    }
    }                                        

    private void btnExtraccionActionPerformed(java.awt.event.ActionEvent evt) {                                              
AGusuario abrir= new AGusuario();
        abrir.setVisible(true);
         dispose();

   
    }                                             
    
    /**
     * @param args the command line arguments
     */
    public static void main(String args[]) {
        /* Set the Nimbus look and feel */
        //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
        /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
         * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
         */
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(Abre_Cualquier_Archivo.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(Abre_Cualquier_Archivo.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(Abre_Cualquier_Archivo.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(Abre_Cualquier_Archivo.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>

        /* Create and display the form */
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new Abre_Cualquier_Archivo().setVisible(true);
            }
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton btnExtraccion;
    private javax.swing.JButton jButton1;
    private javax.swing.JLabel jLabel1;
    // End of variables declaration                   
}
CÓDIGO MDI PARA MOSTRAR, MODIFICAR Y ELIMINAR BASE DE DATOS

package ctruser;

import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import javax.swing.JOptionPane;
import javax.swing.table.DefaultTableModel;


public class IngresoForm extends javax.swing.JInternalFrame {
    
      private usuario ingreso=null;
    
    public IngresoForm() {
     initComponents();
     
       
        ingreso = new usuario();       
    }
private void llenaG(){
    ResultSet rs= ingreso.getConsulta();
    DefaultTableModel modelo=(DefaultTableModel)datos.getModel();// SE NECESITA UN MODELO STANDAR, se crea un objet default llamdo modelo
   // mi modelo va a ser igual a datos , getmodel me da un objeto de tipo tablemodel, pongo un cas para convertirlo en a default
    while(modelo.getRowCount()>0) modelo.removeRow(0);//condición cuantos renglones tenemos para que actualice tabla
    int id;
    String usuario,clave;
    String Nombre;
    int IdUsuario;
    int NumSeguidores;
    int NumAmigos;
    
    String query=("select = from persona");// 
    try{
    while(rs.next()){
     
        id=rs.getInt("id");
        
        usuario=rs.getString("usuario");
        clave=rs.getString("clave");     
        Nombre=rs.getString("Nombre");// 
        IdUsuario=rs.getInt("IdUsuario");
        NumSeguidores=rs.getInt("NumSeguidores");       
        NumAmigos=rs.getInt("NumAmigos");
        
        
        
         //System.out.println("Nombre: "+Nombre +"\nApellido: "+ apellido);
        //System.out.println(Nombre);
        
     //modelo.addRow(new Object[]{id,usuario, clave});// agrego una fila con arreglo de objetos por 
    modelo.addRow(new Object[]{id,usuario,clave,Nombre, IdUsuario,NumSeguidores, NumAmigos });
    
   // modelo.addRow(new Object[]{rs.getInt("id") +"\t\t"+ rs.getString("NOMBRE_COMPLETO")+"\t"+ rs.getString("ID_USUARIO")+ "\t"+ rs.getString("NUM_SEGUIDORES")+ "\t"+ rs.getInt("NUM_AMIGOS")});
  
    }
}catch (SQLException e){
    System.out.println(e);
}
}
    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jPanel1 = new javax.swing.JPanel();
        btnNuevo = new javax.swing.JButton();
        btnExtraer = new javax.swing.JButton();
        btnEliminar = new javax.swing.JButton();
        btnMostrar = new javax.swing.JButton();
        jScrollPane1 = new javax.swing.JScrollPane();
        datos = new javax.swing.JTable();

        setClosable(true);
        setIconifiable(true);
        setMaximizable(true);
        setResizable(true);
        setTitle("CONTROL DE  BASE DE DATOS");

        jPanel1.setBackground(new java.awt.Color(102, 102, 255));

        btnNuevo.setText("AÑADIR");
        btnNuevo.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnNuevoActionPerformed(evt);
            }
        });

        btnExtraer.setText("INFORMACION");
        btnExtraer.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnExtraerActionPerformed(evt);
            }
        });

        btnEliminar.setText("ELIMINAR");
        btnEliminar.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnEliminarActionPerformed(evt);
            }
        });

        btnMostrar.setText("MOSTRAR");
        btnMostrar.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btnMostrarActionPerformed(evt);
            }
        });

        datos.setModel(new javax.swing.table.DefaultTableModel(
            new Object [][] {

            },
            new String [] {
                "id", "usuario", "clave", "Nombre", "IdUsuario ", "NumSeguidores ", "NumAmigos "
            }
        ) {
            boolean[] canEdit = new boolean [] {
                false, false, false, false, false, false, false
            };

            public boolean isCellEditable(int rowIndex, int columnIndex) {
                return canEdit [columnIndex];
            }
        });
        datos.setSelectionForeground(new java.awt.Color(200, 200, 200));
        datos.setUpdateSelectionOnSort(false);
        datos.addMouseListener(new java.awt.event.MouseAdapter() {
            public void mouseClicked(java.awt.event.MouseEvent evt) {
                datosMouseClicked(evt);
            }
        });
        datos.addKeyListener(new java.awt.event.KeyAdapter() {
            public void keyPressed(java.awt.event.KeyEvent evt) {
                datosKeyPressed(evt);
            }
        });
        jScrollPane1.setViewportView(datos);

        javax.swing.GroupLayout jPanel1Layout = new javax.swing.GroupLayout(jPanel1);
        jPanel1.setLayout(jPanel1Layout);
        jPanel1Layout.setHorizontalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel1Layout.createSequentialGroup()
                .addGap(38, 38, 38)
                .addComponent(btnExtraer)
                .addGap(88, 88, 88)
                .addComponent(btnMostrar, javax.swing.GroupLayout.PREFERRED_SIZE, 91, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, 98, Short.MAX_VALUE)
                .addComponent(btnNuevo, javax.swing.GroupLayout.PREFERRED_SIZE, 91, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(86, 86, 86)
                .addComponent(btnEliminar, javax.swing.GroupLayout.PREFERRED_SIZE, 91, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(44, 44, 44))
            .addComponent(jScrollPane1, javax.swing.GroupLayout.Alignment.TRAILING)
        );
        jPanel1Layout.setVerticalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel1Layout.createSequentialGroup()
                .addGap(19, 19, 19)
                .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(btnEliminar)
                    .addComponent(btnNuevo)
                    .addComponent(btnMostrar)
                    .addComponent(btnExtraer))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, 30, Short.MAX_VALUE)
                .addComponent(jScrollPane1, javax.swing.GroupLayout.PREFERRED_SIZE, 345, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addContainerGap())
        );

        getContentPane().add(jPanel1, java.awt.BorderLayout.PAGE_START);

        pack();
    }// </editor-fold>                        

    private void btnMostrarActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // TODO add your handling code here:
      llenaG();
    }                                          

    private void btnEliminarActionPerformed(java.awt.event.ActionEvent evt) {                                            
     
    int row= datos.getSelectedRow();
   
    DefaultTableModel modelo=(DefaultTableModel)datos.getModel();
    
    String ID =  modelo.getValueAt(row,0).toString();
    
    int r = ingreso.eliminaUse(ID);
    
    if (r!=0){
    JOptionPane.showMessageDialog(null, "el registro se eliminó correctaente");
    this.llenaG();
    
}else{
    JOptionPane.showMessageDialog(null, " Error al eliminar");
}
    
    }                                           
 
    
    
    private void btnExtraerActionPerformed(java.awt.event.ActionEvent evt) {                                           
         this.dispose();
       Abre_Cualquier_Archivo i= new Abre_Cualquier_Archivo();
        i.setVisible(true);  
     
        
    }                                          

    private void btnNuevoActionPerformed(java.awt.event.ActionEvent evt) {                                         
       AGusuario abrir= new AGusuario();
        abrir.setVisible(true);       
       llenaG();// llamamos este metodo para que uando se agregue una fila se actualice en el MDI de bd
    }                                        

    private void datosMouseClicked(java.awt.event.MouseEvent evt) {                                   
      
        

        // TODO add your handling code here:
    }                                  

    private void datosKeyPressed(java.awt.event.KeyEvent evt) {                                 

  
    
        // TODO add your handling code here:
    }                                


    // Variables declaration - do not modify                     
    private javax.swing.JButton btnEliminar;
    private javax.swing.JButton btnExtraer;
    private javax.swing.JButton btnMostrar;
    private javax.swing.JButton btnNuevo;
    private javax.swing.JTable datos;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JScrollPane jScrollPane1;
    // End of variables declaration                  
    }
CÓDIGO DE LOGIN
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package ctruser;

import java.awt.HeadlessException;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import javax.swing.JOptionPane;

/**
 *
 * @author ShirleyDelRosario
 */
public class LOGIN extends javax.swing.JFrame {
    
SSMP cc= new SSMP();
Connection con =SSMP.getConnection();
    /**
     * Creates new form AGusuario
     */
    public LOGIN() {
        initComponents();
       this.setTitle("Registro usuario");
       this.setLocation(300, 220);//centramos el jframe con titulo
       
    }

    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jLabel1 = new javax.swing.JLabel();
        txtUsuario = new javax.swing.JTextField();
        jLabel2 = new javax.swing.JLabel();
        btningresar = new javax.swing.JButton();
        txtclave = new javax.swing.JPasswordField();
        jLabel4 = new javax.swing.JLabel();
        jLabel3 = new javax.swing.JLabel();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
        setPreferredSize(new java.awt.Dimension(507, 300));

        jLabel1.setFont(new java.awt.Font("Arial Black", 0, 18)); // NOI18N
        jLabel1.setText("USUARIO");

        jLabel2.setFont(new java.awt.Font("Arial Black", 0, 18)); // NOI18N
        jLabel2.setText("PASSWORD");

        btningresar.setText("INGRESAR");
        btningresar.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btningresarActionPerformed(evt);
            }
        });

        txtclave.setText("jPasswordField1");

        jLabel4.setBackground(new java.awt.Color(255, 255, 51));
        jLabel4.setFont(new java.awt.Font("Arial Black", 0, 14)); // NOI18N
        jLabel4.setForeground(new java.awt.Color(102, 102, 255));
        jLabel4.setText("CONTROL DE INFORMACIÓN");

        jLabel3.setIcon(new javax.swing.ImageIcon(getClass().getResource("/inf.jpg"))); // NOI18N
        jLabel3.setText("jLabel3");

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addGap(45, 45, 45)
                        .addComponent(jLabel1)
                        .addGap(39, 39, 39))
                    .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                        .addContainerGap()
                        .addComponent(jLabel2)
                        .addGap(18, 18, 18)))
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addComponent(txtUsuario, javax.swing.GroupLayout.PREFERRED_SIZE, 156, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(18, 18, 18)
                        .addComponent(btningresar, javax.swing.GroupLayout.PREFERRED_SIZE, 109, javax.swing.GroupLayout.PREFERRED_SIZE))
                    .addComponent(txtclave, javax.swing.GroupLayout.PREFERRED_SIZE, 148, javax.swing.GroupLayout.PREFERRED_SIZE)))
            .addComponent(jLabel3, javax.swing.GroupLayout.PREFERRED_SIZE, 657, javax.swing.GroupLayout.PREFERRED_SIZE)
            .addGroup(layout.createSequentialGroup()
                .addGap(92, 92, 92)
                .addComponent(jLabel4))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addComponent(jLabel3, javax.swing.GroupLayout.PREFERRED_SIZE, 126, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(3, 3, 3)
                .addComponent(jLabel4, javax.swing.GroupLayout.PREFERRED_SIZE, 33, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(18, 18, 18)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(btningresar, javax.swing.GroupLayout.PREFERRED_SIZE, 42, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addGroup(layout.createSequentialGroup()
                        .addComponent(txtUsuario, javax.swing.GroupLayout.PREFERRED_SIZE, 26, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                            .addComponent(txtclave, javax.swing.GroupLayout.PREFERRED_SIZE, 26, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(jLabel2)))
                    .addComponent(jLabel1))
                .addContainerGap(38, Short.MAX_VALUE))
        );

        pack();
    }// </editor-fold>                        

    private void btningresarActionPerformed(java.awt.event.ActionEvent evt) {                                            
        // TODO add your handling code here:
       Validarusuario(); 
    }                                           
public void Validarusuario(){
 
    int resultado=0;
    
    String clave=String.valueOf(txtclave.getPassword());
    
    String usuario=txtUsuario.getText();
      // selecciona los datos de la BD si el usuario y contraseña coinciden o se encuentra dentro de mi BD
    String SQL= "select * from persona where usuario= '"+usuario+"'  and clave ='"  +clave+"'";
    try{
        Statement st=con.createStatement();
        ResultSet rs=st.executeQuery(SQL);
        if(rs.next()){
            resultado=1;
            if(resultado==1){
                MDIprincipal form= new MDIprincipal();
                form.setVisible(true);
               // this.dispone();// cierra ventana
            }
        }else{
             JOptionPane.showMessageDialog(null,"Error de acceso, usuario no registrado");
        }
        
    }catch(HeadlessException | SQLException e){
        
        JOptionPane.showMessageDialog(null,"Error" + e.getMessage());
    }
   
}
    
    
    
    
    
    
    /**
     * @param args the command line arguments
     */
    public static void main(String args[]) {
        /* Set the Nimbus look and feel */
        //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
        /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
         * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
         */
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(LOGIN.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(LOGIN.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(LOGIN.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(LOGIN.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>
        //</editor-fold>

        /* Create and display the form */
        java.awt.EventQueue.invokeLater(() -> {
            new LOGIN().setVisible(true);
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton btningresar;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel2;
    private javax.swing.JLabel jLabel3;
    private javax.swing.JLabel jLabel4;
    private javax.swing.JTextField txtUsuario;
    private javax.swing.JPasswordField txtclave;
    // End of variables declaration                   

    private void dispone() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

   
}
CÓDIGO MDI PRINCIPAL
package ctruser;
/**
 *
 * @author ShirleyDelRosario
 */
public class MDIprincipal extends javax.swing.JFrame {
private IngresoForm use = null;
    /**
     * Creates new form MDIprincipal
     */
    public MDIprincipal() {
        initComponents();
       this.setTitle("Registro usuario");
       this.setLocation(400, 220);//centramos el jframe con titulo
    }
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        desktopPane = new javax.swing.JDesktopPane();
        jLabel1 = new javax.swing.JLabel();
        menuBar = new javax.swing.JMenuBar();
        fileMenu = new javax.swing.JMenu();
        ingresoMenuItem = new javax.swing.JMenuItem();
        saveMenuItem = new javax.swing.JMenuItem();
        saveAsMenuItem = new javax.swing.JMenuItem();
        exitMenuItem = new javax.swing.JMenuItem();
        editMenu = new javax.swing.JMenu();
        cutMenuItem = new javax.swing.JMenuItem();
        copyMenuItem = new javax.swing.JMenuItem();
        pasteMenuItem = new javax.swing.JMenuItem();
        deleteMenuItem = new javax.swing.JMenuItem();
        helpMenu = new javax.swing.JMenu();
        contentMenuItem = new javax.swing.JMenuItem();
        aboutMenuItem = new javax.swing.JMenuItem();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        jLabel1.setIcon(new javax.swing.ImageIcon(getClass().getResource("/RED.png"))); // NOI18N
        jLabel1.setText("jLabel1");
        desktopPane.add(jLabel1);
        jLabel1.setBounds(0, 0, 400, 280);

        fileMenu.setMnemonic('f');
        fileMenu.setText("ARCHIVO");

        ingresoMenuItem.setMnemonic('o');
        ingresoMenuItem.setText("TWITTER");
        ingresoMenuItem.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                ingresoMenuItemActionPerformed(evt);
            }
        });
        fileMenu.add(ingresoMenuItem);

        saveMenuItem.setMnemonic('s');
        saveMenuItem.setText("FACEBOOK");
        fileMenu.add(saveMenuItem);

        saveAsMenuItem.setMnemonic('a');
        saveAsMenuItem.setText("INSTAGRAM");
        fileMenu.add(saveAsMenuItem);

        exitMenuItem.setMnemonic('x');
        exitMenuItem.setText("Exit");
        exitMenuItem.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                exitMenuItemActionPerformed(evt);
            }
        });
        fileMenu.add(exitMenuItem);

        menuBar.add(fileMenu);

        editMenu.setMnemonic('e');
        editMenu.setText("Edit");

        cutMenuItem.setMnemonic('t');
        cutMenuItem.setText("Cut");
        editMenu.add(cutMenuItem);

        copyMenuItem.setMnemonic('y');
        copyMenuItem.setText("Copy");
        editMenu.add(copyMenuItem);

        pasteMenuItem.setMnemonic('p');
        pasteMenuItem.setText("Paste");
        editMenu.add(pasteMenuItem);

        deleteMenuItem.setMnemonic('d');
        deleteMenuItem.setText("Delete");
        editMenu.add(deleteMenuItem);

        menuBar.add(editMenu);

        helpMenu.setMnemonic('h');
        helpMenu.setText("Help");

        contentMenuItem.setMnemonic('c');
        contentMenuItem.setText("Contents");
        helpMenu.add(contentMenuItem);

        aboutMenuItem.setMnemonic('a');
        aboutMenuItem.setText("About");
        helpMenu.add(aboutMenuItem);

        menuBar.add(helpMenu);

        setJMenuBar(menuBar);

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addComponent(desktopPane, javax.swing.GroupLayout.DEFAULT_SIZE, 400, Short.MAX_VALUE)
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addComponent(desktopPane, javax.swing.GroupLayout.DEFAULT_SIZE, 279, Short.MAX_VALUE)
        );

        pack();
    }// </editor-fold>                        

    private void exitMenuItemActionPerformed(java.awt.event.ActionEvent evt) {                                             
        System.exit(0);
    }                                            

    private void ingresoMenuItemActionPerformed(java.awt.event.ActionEvent evt) {                                                
        // TODO add your handling code here:
        if(use == null || use.isClosed()){
            use=new IngresoForm();
           
            this.desktopPane.add(use);
            
        }
        use.setVisible(true);
        
                                
    }                                               

    /**
     * @param args the command line arguments
     */
    public static void main(String args[]) {
        /* Set the Nimbus look and feel */
        //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
        /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
         * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
         */
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(MDIprincipal.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(MDIprincipal.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(MDIprincipal.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(MDIprincipal.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>

        /* Create and display the form */
        java.awt.EventQueue.invokeLater(() -> {
            new MDIprincipal().setVisible(true);
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.JMenuItem aboutMenuItem;
    private javax.swing.JMenuItem contentMenuItem;
    private javax.swing.JMenuItem copyMenuItem;
    private javax.swing.JMenuItem cutMenuItem;
    private javax.swing.JMenuItem deleteMenuItem;
    private javax.swing.JDesktopPane desktopPane;
    private javax.swing.JMenu editMenu;
    private javax.swing.JMenuItem exitMenuItem;
    private javax.swing.JMenu fileMenu;
    private javax.swing.JMenu helpMenu;
    private javax.swing.JMenuItem ingresoMenuItem;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JMenuBar menuBar;
    private javax.swing.JMenuItem pasteMenuItem;
    private javax.swing.JMenuItem saveAsMenuItem;
    private javax.swing.JMenuItem saveMenuItem;
    // End of variables declaration                   

   

}





