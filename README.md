package DAO;

import Conexao.ConexaoComMySQL;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;
import beans.Edital;


//classe Data Acess Object. Criar uma classe DOA para cada classe bean.
//Exemplo com classe Categoria.



public class EditalDAO {
    


    private Connection conexao=null;

    public EditalDAO () {
    conexao = ConexaoComMySQL.getConexaoMySQL();
    }
    
    //inserir
    public boolean insert(Edital Edital){ 
        String sql = "INSERT INTO edital (  id_edital,  dt_inicio, dt_fim,  dt_recurso,  dt_publicacao) VALUES (?,?,?,?,?,?)";
        PreparedStatement statement = null;
        try{
        statement = conexao.prepareStatement(sql);
        
        statement.setInt(1,Edital.getId_edital()); 
        statement.setString(2,Edital.getDt_inicio() );
        statement.setString(3, Edital.getDt_fim());
        statement.setString(4, Edital.getDt_recurso()); 
        statement.setString(5, Edital.getDt_publicacao());
        
        
        statement.executeUpdate();
        return true;
    }catch (SQLException e){
            System.out.println("erro: "+e);
            return false;
    }finally{
            //fechar conexao
            ConexaoComMySQL.FecharConexao();
        }
    }


}
